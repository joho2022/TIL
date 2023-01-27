# TimeBasedOperators
<br/><br/><br/><br/>
 

```Swift
import RxSwift

let disposeBag = DisposeBag()

// replay : 지나간 이벤트라도 버퍼의 숫자만큼 최신의 값을 받을 수 있다. 구독자가 과거의 요소들을 자기가 구독하기 전에 나왔던 이벤트들도 버퍼의 갯수만큼 최신 요소대로 받을 수 있다.
print("------replay-------")
let 인사말 = PublishSubject<String>()
let 반복하는앵무새 = 인사말.replay(1)
반복하는앵무새.connect() //replay 관련한 연산자를 쓸때는 반드시 connect를 해주어야 함

인사말.onNext("1. hello")
인사말.onNext("2. hi")

반복하는앵무새
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

인사말.onNext("3. 안녕하세요") // 구독된 시점 이후에 발생한 이벤트는 버퍼의 크기와 상관없이 무조건 나타나게 된다.

print("----------replayAll----------")
let 닥터스트레인지 = PublishSubject<String>()
let 닥터스트레인지의타임스톤 = 닥터스트레인지.replayAll()
닥터스트레인지의타임스톤.connect()

닥터스트레인지.onNext("도르마무")
닥터스트레인지.onNext("거래를 하러왔다")

닥터스트레인지의타임스톤
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

// 리턴값이 어레이
//print("----------buffer----------")
//let source = PublishSubject<String>()
//
//var count = 0
//let timer = DispatchSource.makeTimerSource()
//timer.schedule(deadline: .now() + 2, repeating: .seconds(1))
//timer.setEventHandler {
//    count += 1
//    source.onNext("\(count)")
//}
//timer.resume()
//
//source
//    .buffer(
//        timeSpan: .seconds(2),
//        count: 2,
//        scheduler: MainScheduler.instance
//    )
//    .subscribe(onNext: {
//        print($0)
//    })
//    .disposed(by: disposeBag)

//리턴값이 옵저버블
//print("----------window----------")
//let 만들어낼최대Observable수 = 1
//let 만들시간 = RxTimeInterval.seconds(2)
//
//let window = PublishSubject<String>()
//
//var windowCount = 0
//let windowTimerSource = DispatchSource.makeTimerSource()
//windowTimerSource.schedule(deadline: .now() + 2, repeating: .seconds(1))
//windowTimerSource.setEventHandler {
//    windowCount += 1
//    window.onNext("\(delayCount)")
//}
//windowTimerSource.resume()
//
//window
//    .window(
//        timeSpan: 만들시간,
//        count: 만들어낼최대Observable수,
//        scheduler: MainScheduler.instance
//    )
//    .flatMap { windowObservable -> Observable<(index: Int, element: String)> in
//        return windowObservable.enumerated()
//    }
//    .subscribe(onNext: {
//        print("\($0.index)번째 Observable의 요소 \($0.element)")
//    })
//    .disposed(by: disposeBag)

// delaySubscription : 소스는 돌아가지만 구독이 지연되는 느낌
//print("----------delaySubscription----------")
//let delaySource = PublishSubject<String>()
//
//var delayCount = 0
//let delayTimerSource = DispatchSource.makeTimerSource()
//delayTimerSource.schedule(deadline: .now() + 2, repeating: .seconds(1))
//delayTimerSource.setEventHandler {
//    delayCount += 1
//    delaySource.onNext("\(delayCount)")
//}
//delayTimerSource.resume()
//
//delaySource
//    .delaySubscription(.seconds(2), scheduler: MainScheduler.instance)
//    .subscribe(onNext: {
//        print($0)
//    })
//    .disposed(by: disposeBag)

// delay : 시퀀스 자체가 뒤로 미루는 느낌
//print("----------delay----------")
//let delaySubject = PublishSubject<Int>()
//
//var delaySubjectCount = 0
//let delaySubjectTimerSource = DispatchSource.makeTimerSource()
//delaySubjectTimerSource.schedule(deadline: .now(), repeating: .seconds(1))
//delaySubjectTimerSource.setEventHandler {
//    delaySubjectCount += 1
//    delaySubject.onNext(delaySubjectCount)
//}
//delaySubjectTimerSource.resume()
//
//delaySubject
//    .delay(.seconds(3), scheduler: MainScheduler.instance)
//    .subscribe(onNext: {
//        print($0)
//    })
//    .disposed(by: disposeBag)


//print("----------interval----------")
//Observable<Int>
//    .interval(.seconds(3), scheduler: MainScheduler.instance)
//    .subscribe(onNext: {
//        print($0)
//    })
//    .disposed(by: disposeBag)

print("----------timer----------")
Observable<Int>
    .timer(
        .seconds(5),    //구독 시작 딜레이
        period: .seconds(2),    //간격
        scheduler: MainScheduler.instance
    )
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

//print("----------timeout----------")
//let 누르지않으면에러 = UIButton(type: .system)
//누르지않으면에러.setTitle("눌러주세요!", for: .normal)
//누르지않으면에러.sizeToFit()
//
//PlaygroundPage.current.liveView = 누르지않으면에러
//
//누르지않으면에러.rx.tap
//    .do(onNext: {
//        print("tap")
//    })
//    .timeout(.seconds(5), scheduler: MainScheduler.instance)
//    .subscribe {
//        print($0)
//    }
//    .disposed(by: disposeBag)


```

<br/><br/><br/>



<br/><br/><br/><br/>
* * *
## Reference
https://fastcampus.co.kr/

