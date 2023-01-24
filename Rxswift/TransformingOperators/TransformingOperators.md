# RxSwift
<br/><br/><br/><br/>
```Swift
import RxSwift

let disposeBag = DisposeBag()

print("-----toArray-----")
Observable.of("A", "B", "C")
    .toArray()
    .subscribe(onSuccess: {
        print($0)
    })
    .disposed(by: disposeBag)

print("--------map--------")
Observable.of(Date())
    .map { date -> String in
        let dateFormatter = DateFormatter()
        dateFormatter.dateFormat = "yyyy-MM-dd"
        dateFormatter.locale = Locale(identifier: "ko_KR")
        return dateFormatter.string(from: date)
    }
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

print("--------flatMap--------")
protocol 선수 {
    var 점수: BehaviorSubject<Int> { get }
}

struct 양궁선수: 선수 {
    var 점수: BehaviorSubject<Int>
}

let 🇰🇷국가대표 = 양궁선수(점수: BehaviorSubject(value: 10))
let 🇺🇸국가대표 = 양궁선수(점수: BehaviorSubject(value: 8))

let 올림픽경기 = PublishSubject<선수>()

올림픽경기
    .flatMap { 선수 in
        선수.점수
    }
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

올림픽경기.onNext(🇰🇷국가대표)
🇰🇷국가대표.점수.onNext(10)

올림픽경기.onNext(🇺🇸국가대표)
🇰🇷국가대표.점수.onNext(10)
🇺🇸국가대표.점수.onNext(9)

print("--------flatMapLatest--------")
struct 높이뛰기선수: 선수 {
    var 점수: BehaviorSubject<Int>
}

let 서울 = 높이뛰기선수(점수: BehaviorSubject<Int>(value: 7))
let 제주 = 높이뛰기선수(점수: BehaviorSubject<Int>(value: 6))

let 전국체전 = PublishSubject<선수>()

전국체전
    .flatMapLatest { 선수 in
        선수.점수
    }
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

전국체전.onNext(서울)
서울.점수.onNext(9)

전국체전.onNext(제주)
서울.점수.onNext(10)
// 왜 10은 안 나와요? : 전국체전의 입장에서 서울만의 sequence을 가지고 있을 때 최신값을 가지고 그다음 제주 sequence 새로운 sequence가 발생한 이후부터는 서울은 해제된다. 이후에 서울이 새로운 값을 내도 받아주지 않기 때문에 10이 안나온다.
제주.점수.onNext(8)

// 예시 : 사전으로 단어를 찾는 것을 생각해보자 ..  s -> String, sw -> switch

print("--------materialize and dematerialize--------")
enum 반칙: Error {
    case 부정출발
}

struct 달리기선수: 선수 {
    var 점수: BehaviorSubject<Int>
}

let 김토끼 = 달리기선수(점수: BehaviorSubject(value: 0))
let 박치타 = 달리기선수(점수: BehaviorSubject(value: 1))

let 달리기100M = BehaviorSubject<선수>(value: 김토끼)

달리기100M
    .flatMapLatest {
        $0.점수
            .materialize()    // 1) materialize 추가
    }
//     2) demeterialize 추가
    .filter {
        guard let error = $0.error else {
            return true
        }
        print(error)
        return false
    }
    .dematerialize()
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

김토끼.점수.onNext(1)
김토끼.점수.onError(반칙.부정출발)
김토끼.점수.onNext(2)

달리기100M.onNext(박치타)

print("--------전화번호 11자리--------")
let input = PublishSubject<Int?>()

let list: [Int] = [1]

input
    .flatMap {
        $0 == nil
        ? Observable.empty()
        : Observable.just($0)
    }
    .map { $0! }
    .skip(while: { $0 != 0 })
    .take(11)
    .toArray()
    .asObservable()
    .map {
        $0.map { "\($0)" }
    }
    .map { numbers in
        var numberList = numbers
        numberList.insert("-", at: 3) // 010-
        numberList.insert("-", at: 8) // 010-1234-
        let number = numberList.reduce(" ", +) // 각각의 스트링을 더한다
        return number
    }
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

input.onNext(10)
input.onNext(0)
input.onNext(nil)
input.onNext(1)
input.onNext(0)
input.onNext(4)
input.onNext(3)
input.onNext(nil)
input.onNext(1)
input.onNext(8)
input.onNext(9)
input.onNext(4)
input.onNext(9)
input.onNext(4)


```

<br/><br/><br/>

## 결과
```
-----toArray-----
["A", "B", "C"]
--------map--------
2023-01-24
--------flatMap--------
10
10
8
10
9
--------flatMapLatest--------
7
9
6
8
--------materialize and dematerialize--------
0
1
부정출발
1
--------전화번호 11자리--------
 010-4318-9494

```

<br/><br/><br/><br/>
* * *
## Reference
https://fastcampus.co.kr/

