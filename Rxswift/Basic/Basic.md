# RxSwift
<br/><br/><br/><br/>
```
import Foundation //기본 프레임워크다.
import RxSwift

// just : 단순히 하나만 생성하는 Oservable Sequence
// Observable은 Sequence의 정의일 뿐 구독되기 전까지는 아무런 이벤트가 발생되지 않는다.
print("----just----")
Observable<Int>.just(1)
    .subscribe(onNext: {
        print($0)
    })

// of: 하나 이상을 생성하는 Observable Sequence
print("----Of1----")
Observable<Int>.of(1, 2, 3, 4, 5)
    .subscribe(onNext: {
        print($0)
    })

print("----Of1----") // just와 같이 배열 하나만 생성
Observable.of([1, 2, 3, 4, 5])
    .subscribe(onNext: {
        print($0)
    })

print("----From----") // from : 자기가 받은 array속에 있는 elements를 꺼내서 방출함
Observable.from([1, 2, 3, 4, 5])
    .subscribe(onNext: {
        print($0)
    })

print("------subscribe1-------")
Observable.of(1,2,3)
    .subscribe {
        
        print($0)
    }


print("------subscribe2-------")
Observable.of(1,2,3)
    .subscribe {
        if let element = $0.element {
            print(element)
        }
    }

print("------subscribe3-------")
Observable.of(1,2,3)
    .subscribe(onNext: {
        print($0)
    }) // onNext를 통한 element만 방출하기 때문에 element받을 수 있는 것을 확인할 수 있다.

print("------empty-------")
Observable<Void>.empty()  //empty : 아무런 elemet가지지 않고 이벤트를 방출하지 않는다.
    .subscribe {         //empty의 용도는?? 1. 즉시 종료할 수 있는 Observable을 리턴하고 싶을 때
        //              2. 의도적으로 0개의 값을 가지는 Observable을 리턴하고 싶을 때
        print($0)
    }

print("-------never------")
Observable<Void>.never()  //타입을 추론할 수 있게 적었음에도 불구하고 아무것도 print되지 않는다.
    .debug("never")
    .subscribe(onNext: {
        print($0)
    }, onCompleted: {
        print("Completed  ")
    })

print("-----range-------")
Observable.range(start: 1, count: 9)
    .subscribe(onNext: {
        print("2*\($0)=\(2*$0)")
    })

// 즉, subscribe은 Observable이 방출될 수 있도록 방아쇠역할을 해준다.

print("-----dispose------")
Observable.of(1, 2, 3)
    .subscribe(onNext: {
        print($0)
    })
    .dispose()
// dispose : 구독취소권같은 것, 사용하지 않으면 observable이 사라지지 않아서 메모리 누수가 발생.

print("-----disposeBag------")
let disposeBag = DisposeBag()

Observable.of(1, 2, 3)
    .subscribe {
        print($0)
    }
    .disposed(by: disposeBag)
// disposeBag: Observable 구독의 수가 많아지면 이를 개별적으로 관리해주는 것도 일인데, 이런 상황을 disposeBag으로 한꺼번에 관리가 가능하다.

print("-----create1-----")
Observable.create { observer -> Disposable in
    observer.onNext(1)
    //    observer.on(.next(1))
    observer.onCompleted()
    //    observer.on(.completed)
    observer.onNext(2)
    return Disposables.create()
}
.subscribe {
    print($0)
}
.disposed(by: disposeBag)

// 2번째 element가 방출되지 않은 이유: onCompleted를 통해서 observer이 종료되었기 때문에


print("-----create2-----")
enum MyError: Error {
case anError
}

Observable<Int>.create { observer -> Disposable in
    observer.onNext(1)
    observer.onError(MyError.anError)
    observer.onCompleted()
    observer.onNext(2)
    return Disposables.create()
}
.subscribe(
    onNext: {
        print($0)
    },
    onError: {
        print($0.localizedDescription)
    },
    onCompleted: {
        print("completed")
    },
    onDisposed: {
        print("disposed")
    }
)
.disposed(by: disposeBag)


print("-----deffered1-----")
Observable.deferred {
    Observable.of(1, 2, 3)
}
.subscribe {
    print($0)
}
.disposed(by: disposeBag)

print("-----deffered2-----")
var 뒤집기: Bool = false

let fatory: Observable<String> = Observable.deferred{
    뒤집기 = !뒤집기
    
    if 뒤집기 {
        return Observable.of("🤲")
    } else {
        return Observable.of("🙌")
    }
}

for _ in 0...3 {
    fatory.subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)
}

```

<br/><br/><br/>

## 결과
```
----just----
1
----Of1----
1
2
3
4
5
----Of1----
[1, 2, 3, 4, 5]
----From----
1
2
3
4
5
------subscribe1-------
next(1)
next(2)
next(3)
completed
------subscribe2-------
1
2
3
------subscribe3-------
1
2
3
------empty-------
completed
-------never------
2023-01-21 13:07:02.893: never -> subscribed
-----range-------
2*1=2
2*2=4
2*3=6
2*4=8
2*5=10
2*6=12
2*7=14
2*8=16
2*9=18
-----dispose------
1
2
3
-----disposeBag------
next(1)
next(2)
next(3)
completed
-----create1-----
next(1)
completed
-----create2-----
1
The operation couldn’t be completed. (__lldb_expr_11.MyError error 0.)
disposed
-----deffered1-----
next(1)
next(2)
next(3)
completed
-----deffered2-----
🤲
🙌
🤲
🙌
```

<br/><br/><br/><br/>
* * *
## Reference 
https://fastcampus.co.kr/
