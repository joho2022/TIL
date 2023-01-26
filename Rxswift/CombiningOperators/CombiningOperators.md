# CombiningOperators
<br/><br/><br/><br/>
   
 
```Swift
import RxSwift

let disposeBag = DisposeBag()

// startWith : 원하는 값을 observable sequence앞에 추가해준다.
print("------startWith-------")
let 노랑반 = Observable<String>.of("👧🏼", "🧒🏻", "👦🏽")

노랑반
// enumerated : observable sequence의 값에 인덱스값과 element를 분리해준다.
    .enumerated()
    .map { index, element in
        return element + "어린이" + "\(index)"
    }
    .startWith("👨🏻선생님")
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag )

// concat : startWith와 흡사하나, 여러개의 Element가 추가된다. (앞, 뒤로 모두 가능)
print("----------concat1----------")
let 노랑반어린이들 = Observable.of("👧🏼", "🧒🏻", "👦🏽")
let 선생님 = Observable.of("👨🏻선생님")

let 줄서서걷기 = Observable
    .concat([선생님, 노랑반어린이들])

줄서서걷기
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

print("----------concat2----------")
선생님
    .concat(노랑반어린이들)
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

print("----------concatMap----------") // flatMap의 사용법과 결과물이 유사 그러나 concatMap은 순서가 보장됨
let 어린이집: [String: Observable<String>] = [
    "노랑반": Observable.of("👧🏼", "🧒🏻", "👦🏽"),
    "파랑반": Observable.of("👶🏾", "👶🏻")
]

Observable.of("노랑반", "파랑반")
    .concatMap { 반 in
        어린이집[반] ?? .empty()
    }
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

// merge : 순서를 보장하지 않고 그냥 합친다.
print("----------merge1----------")
let 강북 = Observable.from(["강북구", "성북구", "동대문구", "종로구"])
let 강남 = Observable.from(["강남구", "강동구", "영등포구", "양천구"])

Observable.of(강북, 강남)
    .merge()
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

// maxConCurrent : merge라는 것을 통해서 한번에 받아낼 Observable의 수
print("----------merge2----------")
Observable.of(강남, 강북)
    .merge(maxConcurrent: 1)
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

// combineLatest : 두 Observable 중 하나라도 새로운 값을 방출하게 되면 두 각 소스의 맨 마지막 값을 뽑아서 새로운 값을 방출하게 된다.
print("----------combineLatest1----------")
let 성 = PublishSubject<String>()
let 이름 = PublishSubject<String>()

let 성명 = Observable.combineLatest(성, 이름) { 성, 이름 in
    성 + 이름
}

성명
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

성.onNext("김")
이름.onNext("똘똘")
이름.onNext("영수")
이름.onNext("은영")
성.onNext("박")
성.onNext("이")
성.onNext("조")

print("----------combineLatest2----------")
let 날짜표시형식 = Observable<DateFormatter.Style>.of(.short, .long)
let 현재날짜 = Observable<Date>.of(Date())

let 현재날짜표시 = Observable
    .combineLatest(
        날짜표시형식,
        현재날짜) { 형식, 날짜 -> String in
            let dateFormatter = DateFormatter()
            dateFormatter.dateStyle = 형식
            return dateFormatter.string(from: 날짜)
        }

현재날짜표시
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

print("----------combineLatest3----------")
let lastName = PublishSubject<String>() // 성
let firstName = PublishSubject<String>() // 이름

let fullName = Observable
    .combineLatest([firstName, lastName]) { name in
        name.joined(separator: " ")
    }

fullName
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

lastName.onNext("Kim")
firstName.onNext("Paul")
firstName.onNext("Stella")
firstName.onNext("Lily")

// zip : 방출된 순서가 같은 아이템을 묶어서 하나의 아이템으로 방출한다.
print("----------zip----------")
enum 승패 {
    case 승
    case 패
}

let 승부 = Observable<승패>.of(.승, .승, .패, .승, .패)
let 선수 = Observable<String>.of("🇰🇷", "🇨🇭", "🇺🇸", "🇧🇷", "🇯🇵", "🇨🇳")

let 시험결과 = Observable
    .zip(승부, 선수) { 결과, 대표선수 in
        return 대표선수 + "선수" + " \(결과)"
    }

시험결과
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

// withLatestFrom: 첫번째 Observable에서 아이템이 방출될 때마다 그 아이템을 두번째 Observable의 가장 최근 아이템과 결합해 방출힌다.
print("----------withLatestFrom1----------")
let 💥🔫 = PublishSubject<Void>()
let 달리기선수 = PublishSubject<String>()

💥🔫
    .withLatestFrom(달리기선수)
//    .distinctUntilChanged() : sample처럼 사용할 수 있다.
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

달리기선수.onNext("🏃🏻‍♀️")
달리기선수.onNext("🏃🏻‍♀️ 🏃🏽‍♂️")
달리기선수.onNext("🏃🏻‍♀️ 🏃🏽‍♂️ 🏃🏿")
💥🔫.onNext(Void())
💥🔫.onNext(Void())

// sample : withLatestFrom(_:) 과 distinctUntilChanged()를 합친 것이다.
print("----------sample----------")
let 🏁출발 = PublishSubject<Void>()
let F1선수 = PublishSubject<String>()

F1선수.sample(🏁출발)
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

F1선수.onNext("🏎")
F1선수.onNext("🏎   🚗")
F1선수.onNext("🏎      🚗   🚙")
🏁출발.onNext(Void())
🏁출발.onNext(Void())
🏁출발.onNext(Void())

// amb : 2개의 Observable을 구독하기(지켜보기)는 하지만 둘중에 먼저 방출하는 것이 생기면 나머지에 대해서는 구독을 하지 않는다.
print("----------amb----------")
let 🚌버스1 = PublishSubject<String>()
let 🚌버스2 = PublishSubject<String>()

let 🚏버스정류장 = 🚌버스1.amb(🚌버스2)

🚏버스정류장.subscribe(onNext: {
    print($0)
})
.disposed(by: disposeBag)

// 버스2가 먼저 방출했기 때문에 버스1은 있어도 구독하지 않는다.
🚌버스2.onNext("버스2-승객0: 👩🏾‍💼")
🚌버스1.onNext("버스1-승객0: 🧑🏼‍💼")
🚌버스1.onNext("버스1-승객1: 👨🏻‍💼")
🚌버스2.onNext("버스2-승객1: 👩🏻‍💼")
🚌버스1.onNext("버스1-승객1: 🧑🏻‍💼")
🚌버스2.onNext("버스2-승객2: 👩🏼‍💼")

// switchLatest : 가장 최근 Observable이 방출하는 이벤트를 구독자에게 방출한다. 파라미터가 없어서 주로  Observable을 방출하는 Observable을 사용한다.
//              :  소스 옵저버블로 들어오는 마지막 시퀀스의 아이템만 구독하는 것이 특징
print("----------switchLatest----------")
let 👩🏻‍💻학생1 = PublishSubject<String>()
let 🧑🏽‍💻학생2 = PublishSubject<String>()
let 👨🏼‍💻학생3 = PublishSubject<String>()

let 손들기 = PublishSubject<Observable<String>>()

let 손든사람만말할수있는교실 = 손들기.switchLatest()
손든사람만말할수있는교실
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

손들기.onNext(👩🏻‍💻학생1)
👩🏻‍💻학생1.onNext("👩🏻‍💻학생1: 저는 1번 학생입니다.")
🧑🏽‍💻학생2.onNext("🧑🏽‍💻학생2: 저요 저요!!!")

손들기.onNext(🧑🏽‍💻학생2)
🧑🏽‍💻학생2.onNext("🧑🏽‍💻학생2: 저는 2번이예요!")
👩🏻‍💻학생1.onNext("👩🏻‍💻학생1: 아.. 나 아직 할말 있는데")

손들기.onNext(👨🏼‍💻학생3)
🧑🏽‍💻학생2.onNext("🧑🏽‍💻학생2: 아니 잠깐만! 내가! ")
👩🏻‍💻학생1.onNext("👩🏻‍💻학생1: 언제 말할 수 있죠")
👨🏼‍💻학생3.onNext("👨🏼‍💻학생3: 저는 3번 입니다~ 아무래도 제가 이긴 것 같네요.")

손들기.onNext(👩🏻‍💻학생1)
👩🏻‍💻학생1.onNext("👩🏻‍💻학생1: 아니, 틀렸어. 승자는 나야.")
🧑🏽‍💻학생2.onNext("🧑🏽‍💻학생2: ㅠㅠ")
👨🏼‍💻학생3.onNext("👨🏼‍💻학생3: 이긴 줄 알았는데")
🧑🏽‍💻학생2.onNext("🧑🏽‍💻학생2: 이거 이기고 지는 손들기였나요?")

// reduce : 모든 이벤트를 다 더한 결과 방출한다.
print("----------reduce----------")
Observable.from((1...10))
    .reduce(0) { summary, newValue in
        return summary + newValue
    }
//    .reduce(0, accumulator: +)
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)

// scan : 매번 값이 들어올때마다 그 결과값을 각각 방출한다.
print("----------scan----------")
Observable.from((1...10))
    .scan(0, accumulator: +)
    .subscribe(onNext: {
        print($0)
    })
    .disposed(by: disposeBag)


```

<br/><br/><br/>

## 결과
```
------startWith-------
👨🏻선생님
👧🏼어린이0
🧒🏻어린이1
👦🏽어린이2
----------concat1----------
👨🏻선생님
👧🏼
🧒🏻
👦🏽
----------concat2----------
👨🏻선생님
👧🏼
🧒🏻
👦🏽
----------concatMap----------
👧🏼
🧒🏻
👦🏽
👶🏾
👶🏻
----------merge1----------
강북구
성북구
강남구
동대문구
강동구
종로구
영등포구
양천구
----------merge2----------
강남구
강동구
영등포구
양천구
강북구
성북구
동대문구
종로구
----------combineLatest1----------
김똘똘
김영수
김은영
박은영
이은영
조은영
----------combineLatest2----------
1/27/23
January 27, 2023
----------combineLatest3----------
Paul Kim
Stella Kim
Lily Kim
----------zip----------
🇰🇷선수 승
🇨🇭선수 승
🇺🇸선수 패
🇧🇷선수 승
🇯🇵선수 패
----------withLatestFrom1----------
🏃🏻‍♀️ 🏃🏽‍♂️ 🏃🏿
🏃🏻‍♀️ 🏃🏽‍♂️ 🏃🏿
----------sample----------
🏎      🚗   🚙
----------amb----------
버스2-승객0: 👩🏾‍💼
버스2-승객1: 👩🏻‍💼
버스2-승객2: 👩🏼‍💼
----------switchLatest----------
👩🏻‍💻학생1: 저는 1번 학생입니다.
🧑🏽‍💻학생2: 저는 2번이예요!
👨🏼‍💻학생3: 저는 3번 입니다~ 아무래도 제가 이긴 것 같네요.
👩🏻‍💻학생1: 아니, 틀렸어. 승자는 나야.
----------reduce----------
55
----------scan----------
1
3
6
10
15
21
28
36
45
55

```

<br/><br/><br/><br/>
* * *
## Reference
https://fastcampus.co.kr/

