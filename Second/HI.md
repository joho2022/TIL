# *UITextView의 placeholder만들기*



*UITextField*는 최대 1줄로만 표시가 된다.



[image:569C4ED7-7CE2-4118-9AA0-2E09575D0AB0-48297-000000CC7EDD0375/스크린샷 2023-01-15 오후 9.21.12.png]





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


asdasd
