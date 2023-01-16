UITextView의 placeholder만들기



*UITextField*는 최대 1줄로만 표시가 된다.   




[image:65785103-9F87-45EF-B76D-D121D6D7CB3E-48297-000000CA1F58EA7F/스크린샷 2023-01-15 오후 9.21.12.png]





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

