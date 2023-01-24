# RxSwift
<br/><br/><br/><br/>
```Swift
import RxSwift

let disposeBag = DisposeBag()

enum TraitsError: Error {
    case single
    case maybe
    case completable
}

// onSuccess : Observable의 onNext와 onCompleted을 합친것과 비슷하다.
// onFailure : Observable의 onError와 비슷하다.
print("-------Single1--------")
Single<String>.just("✅")
    .subscribe(onSuccess: {
        print($0)
    },
               onFailure: {
        print("error : \($0)")
    },
               onDisposed: {
        print("disposed")
    }
    )
    .disposed(by: disposeBag)

print("-------Single2--------")
Observable<String>.create { observer -> Disposable in
    observer.onError(TraitsError.single)
    return Disposables.create()
    
}
.asSingle()
.subscribe(
    onSuccess: {
        print($0)
    },
    onFailure: {
        print("error : \($0.localizedDescription)")
    },
    onDisposed: {
        print("disposed")
    }
)
.disposed(by: disposeBag)

print("-------Single3--------")
struct SomeJSON: Decodable {
    let name: String
}

enum JSONError: Error {
    case decodingError
}

let json1 = """
{"name":"park"}
"""

let json2 = """
{"my_name":"jo"}
"""

func decode(json: String) -> Single<SomeJSON> {
    Single<SomeJSON>.create { observer -> Disposable in
        guard let data = json.data(using: .utf8),
              let json = try? JSONDecoder().decode(SomeJSON.self, from: data)
        else {
            observer(.failure(JSONError.decodingError))
            return Disposables.create()
        }
        
        observer(.success(json))
        return Disposables.create()
    }
}

decode(json: json1)
    .subscribe {
        switch $0 {
        case .success(let json):
            print(json.name)
        case .failure(let error):
            print(error)
        }
    }
    .disposed(by: disposeBag)

decode(json: json2)
    .subscribe {
        switch $0 {
        case .success(let json):
            print(json.name)
        case .failure(let error):
            print(error)
        }
    }
    .disposed(by: disposeBag)
// 실패와 성공밖에 없는 네트워크 같은 경우 single을 이용할 수 있다.

print("----------Maybe1----------")
Maybe<String>.just("✅")
    .subscribe(
        onSuccess: {
            print($0)
        },
        onError: {
            print($0)
        },
        onCompleted: {
            print("completed")
        },
        onDisposed: {
            print("disposed")
        }
    )
    .disposed(by: disposeBag)


print("----------Maybe2----------")
let a = Observable<String>.create { observer -> Disposable in
    observer.onError(TraitsError.maybe)
    return Disposables.create()
}
    .asMaybe()
    .subscribe(
        onSuccess: {
            print("성공: \($0)")
        },
        onError: {
            print("에러: \($0)")
        },
        onCompleted: {
            print("completed")
        },
        onDisposed: {
            print("disposed")
        }
    )
    .disposed(by: disposeBag)

// asCompletable가 없다. 사용하고 싶으면 바로 만들어줘야 함
print("------Completable1-----")
Completable.create { observer -> Disposable in
    observer(.error(TraitsError.completable))
    return Disposables.create()
}
.subscribe(
    onCompleted: {
        print("completed")
    },
    onError: {
        print("error: \($0)")
    },
    onDisposed: {
        print("disposed")
    }
)
.disposed(by: disposeBag)

print("------Completable2-----")
Completable.create { observer -> Disposable in
    observer(.completed)
    return Disposables.create()
}
.subscribe {
    print($0)
}
.disposed(by: disposeBag)

```

<br/><br/><br/>

## 결과
```
-------Single1--------
✅
disposed
-------Single2--------
error : The operation couldn’t be completed. (__lldb_expr_3.TraitsError error 0.)
disposed
-------Single3--------
park
decodingError
----------Maybe1----------
✅
disposed
----------Maybe2----------
에러: maybe
disposed
------Completable1-----
error: completable
disposed
------Completable2-----
completed
```

<br/><br/><br/><br/>
* * *
## Reference
https://fastcampus.co.kr/

