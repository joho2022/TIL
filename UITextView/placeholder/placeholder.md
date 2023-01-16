# UITextView의 placeholder만들기
<br/><br/><br/><br/>


**UITextField**는 최대 1줄로만 표시가 된다.
<br/><br/><br/><br/>


<img width="450" alt="스크린샷 2023-01-15 오후 9 21 12" src="https://user-images.githubusercontent.com/104732020/212664447-e0ba47df-4dfa-4ba6-baab-e94adb287786.png">
위 사진처럼 여러줄을 표현하고 싶을때는??

<br/><br/><br/><br/>



```swift
 //UITextField는 최대줄 수 가 1줄로만 표시됨
    private lazy var textView: UITextView = {
       let textView = UITextView()
        textView.font = .systemFont(ofSize: 15.0)
        textView.text = "문구 입력..."
        textView.textColor = .secondaryLabel
        textView.font = .systemFont(ofSize: 15.0)
        textView.delegate = self
        
        return textView
    }()

extension UploadViewController: UITextViewDelegate {
    func textViewDidBeginEditing(_ textView: UITextView) {
        guard textView.textColor == .secondaryLabel else { return }
        
        textView.text = nil
        textView.textColor = .label
    }
}

```
<br/><br/><br/><br/>

**UITextView**에서 delegate를 사용하여 placeholder를 구현하는 방법을 배웠다.
