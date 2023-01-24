# RxSwift
<br/><br/><br/><br/>
```Swift
import RxSwift

// ignoreElements : next element를 무시한다, completed나 에러같은 이벤트는 허용하나 onNext로 나오는 이벤트는 무시함
print("-----ignoreElements-----")
let 취침모드😴 = PublishSubject<String>()
let disposeBag = DisposeBag()

취침모드😴
    .ignoreElements()
    .subscribe { _ in
        print("☀️")
    }
    .disposed(by: disposeBag)

취침모드😴.onNext("🔊")
취침모드😴.onNext("🔊")
취침모드😴.onNext("🔊")

//취침모드😴.onCompleted()
print("-----elementAt-----")
let 두번울면깨는사람 = PublishSubject<String>()

두번울면깨는사람
    .element(at: 2)  // 받고 싶은 해당되는 인덱스 요소에만 받게 된다. 나머지는 무시한다.
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

두번울면깨는사람.onNext("🔊") //index 0
두번울면깨는사람.onNext("🔊") //index 1
두번울면깨는사람.onNext("🤬") //index 2
두번울면깨는사람.onNext("🔊") //index 3

print("-----filter-----")
Observable.of(1, 2, 3, 4 ,5 ,6 , 7, 8 ) 
    .filter { $0 % 2 == 0 } //특정 조건을 통과되는 것만 얻을 수 있게 한다
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)


print("-----skip-----")
Observable.of("😀", "😃", "😄", "🤓", "😎", "🐶")
    .skip(5) // 첫번째 요소를 기준으로 몇개의 요소를 스킵할 것인지 카운터 값에 넣으면 그만큼 무시하고 내뱉는다.
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

print("-----skipwhile-----")
Observable.of("😀", "😃", "😄", "🤓", "😎", "🐶", "😀", "😃")
    .skip(while: {
        $0 != "🐶" //false가 되면은 그때부터 방출하게 된다.
    })
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)


// 다른 Observable 시동할 때 까지 손님 Observable은 무시하게 된다.
print("-----skipUntil-----")
let 손님 = PublishSubject<String>()
let 문여는시간 = PublishSubject<String>()

손님
    .skip(until: 문여는시간)
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

손님.onNext("😀")
손님.onNext("😃")

문여는시간.onNext("땡")
손님.onNext("😎")

// take : skip의 반대 개념
print("--------take--------")
Observable.of("🥇", "🥈", "🥉", "🤓", "😎")
    .take(3)
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)


print("--------takeWhile--------")
Observable.of("🥇", "🥈", "🥉", "🤓", "😎")
    .take(while: {
        $0 != "🥉"
    })
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

print("--------enumerated--------")
Observable.of("🥇", "🥈", "🥉", "🤓", "😎")
    .enumerated()
    .take(while: {
        $0.index < 3
    })
    .subscribe(onNext: {
        print("\($0.index + 1)번째 선수 \($0.element)메달")
    })
    .disposed(by: disposeBag)

print("--------takeUntil--------")
let 수강신청 = PublishSubject<String>()
let 신청마감 = PublishSubject<String>()
수강신청
    .take(until: 신청마감)
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

수강신청.onNext("🙋🏼‍♀️")
수강신청.onNext("🙋🏻‍♂️")
신청마감.onNext("끝!")
수강신청.onNext("🙋🏻")

// distinctUntilChanged : 연달아 같은 값이 이어질 때 중복되는 값을 막아주는 역할
print("--------distinctUntilChanged1--------")
Observable.of("저는", "저는", "앵무새", "앵무새", "앵무새", "입니다", "입니다", "입니다", "저는", "앵무새", "일까요?", "일까요?")
    .distinctUntilChanged()
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)


```

<br/><br/><br/>

## 결과
```
-----ignoreElements-----
-----elementAt-----
🤬
-----filter-----
2
4
6
8
-----skip-----
🐶
-----skipwhile-----
🐶
😀
😃
-----skipUntil-----
😎
--------take--------
🥇
🥈
🥉
--------takeWhile--------
🥇
🥈
--------enumerated--------
1번째 선수 🥇메달
2번째 선수 🥈메달
3번째 선수 🥉메달
--------takeUntil--------
🙋🏼‍♀️
🙋🏻‍♂️
--------distinctUntilChanged1--------
저는
앵무새
입니다
저는
앵무새
일까요?

* * *
## Reference
https://fastcampus.co.kr/

