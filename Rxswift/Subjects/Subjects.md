# RxSwift
<br/><br/><br/><br/>

```Swift
import RxSwift

let disposeBag = DisposeBag()

print("------publishSubject--------")
let publishSubject = PublishSubject<String>()

// Subject는 observer의 특징지니고 있음 : 이벤트를 내뱉을 수 있다.
publishSubject.onNext("1.안녕하세요")

// observable의 특징을 지니고 있음 : 구독을 해야 의미가 있다.
// 시점에 주목하자! 구독한 시점 이전에 발생한 이벤트에 대해서 전혀 받아들이지 못한 것을 알 수 있다.
let 구독자1 = publishSubject
    .subscribe(onNext: {
        print("첫번째 구독자: \($0)")
    })
    

publishSubject.onNext("2.들리세요?")
publishSubject.on(.next("3.안 들리시나요?"))

구독자1.dispose()

let 구독자2 = publishSubject
    .subscribe(onNext: {
        print("두번째 구독자: \($0)")
    })
    

publishSubject.onNext("4.여보세요 ?")
publishSubject.onCompleted()

publishSubject.onNext("5.끝났나요 ?")

구독자2.dispose()

publishSubject
    .subscribe {
        print("세번째 구독:", $0.element ?? $0)
    }
    .disposed(by: disposeBag)

publishSubject.onNext("6. 찍힐까요  ?")
// 바라보고 있는 observable이 completed되었기 때문에 이후에 구독을 시작하고 onNext를 받았다고해서 이벤트는 받을 수 없다.

print("------behaviorSubject-------")
enum SubjectError: Error {
    case error1
}

let behaviorSubject = BehaviorSubject<String>(value: "초기값")

behaviorSubject.onNext("1. 첫번째값")

behaviorSubject.subscribe {
    print("첫번째 구독: ", $0.element ?? $0)
}
.disposed(by: disposeBag)

//behaviorSubject.onError(SubjectError.error1)

behaviorSubject.subscribe{
    print("두번째 구독: ", $0.element ?? $0)
}
.disposed(by: disposeBag)

let value = try? behaviorSubject.value()
print(value)  // 아직 종료되지 않았기 때문에 가장 최신의 onNext값을 value로 꺼내주는 것을 확인할 수 있다.

print("-----ReplaySubject-----")
let replaySubject = ReplaySubject<String>.create(bufferSize: 2)

replaySubject.onNext("1. 여러분")
replaySubject.onNext("2. 힘내세요")
replaySubject.onNext("3. I CAN DO")

replaySubject.subscribe {
    print("첫번째 구독 : ", $0.element ?? $0 )
}
.disposed(by: disposeBag)

replaySubject.subscribe {
    print("두번째 구독 : ", $0.element ?? $0 )
}
.disposed(by: disposeBag)

replaySubject.onNext("4. 할수 있어요")
replaySubject.onError(SubjectError.error1)
replaySubject.dispose()

replaySubject.subscribe {
    print("세번째 구독 : ", $0.element ?? $0 )
}
.disposed(by: disposeBag)

```

<br/><br/><br/>

## 결과
```
------publishSubject--------
첫번째 구독자: 2.들리세요?
첫번째 구독자: 3.안 들리시나요?
두번째 구독자: 4.여보세요 ?
세번째 구독: completed
------behaviorSubject-------
첫번째 구독:  1. 첫번째값
두번째 구독:  1. 첫번째값
Optional("1. 첫번째값")
-----ReplaySubject-----
첫번째 구독 :  2. 힘내세요
첫번째 구독 :  3. I CAN DO
두번째 구독 :  2. 힘내세요
두번째 구독 :  3. I CAN DO
첫번째 구독 :  4. 할수 있어요
두번째 구독 :  4. 할수 있어요
첫번째 구독 :  error(error1)
두번째 구독 :  error(error1)
세번째 구독 :  error(Object `RxSwift.(unknown context at $10eca9ac0).ReplayMany<Swift.String>` was already disposed.)

```

<br/><br/><br/><br/>
* * *
## Reference
https://fastcampus.co.kr/

