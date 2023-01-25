# refreshControl
<br/><br/><br/><br/>
UITableViewController에는 테이블 새로고침을 할 수 있다.      

<img width="555" alt="스크린샷 2023-01-24 오후 10 22 54" src="https://user-images.githubusercontent.com/104732020/214552671-36a72f7a-fcd0-4c84-9c56-dca409382d87.png">
  
  
```Swift
self.refreshControl = UIRefreshControl()
        let refreshControl = self.refreshControl
        refreshControl?.backgroundColor = .white
        refreshControl?.tintColor = .darkGray
        refreshControl?.attributedTitle = NSAttributedString(string: "당겨서 새로고침")
        refreshControl?.addTarget(self, action: #selector(refresh), for: .valueChanged)
```

<br/><br/><br/>

## 결과
<img width="413" alt="스크린샷 2023-01-25 오후 8 30 56" src="https://user-images.githubusercontent.com/104732020/214552711-ea666f5e-30da-42bc-ad3d-fc1f59c873ea.png">

<br/><br/><br/><br/>
* * *
## Reference

https://developer.apple.com/documentation/uikit/uirefreshcontrol
