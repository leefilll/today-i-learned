## URL Session Delegate

Task의 Response를 다루는 방법 중, Delegate를 이용하는 패턴을 이용

### Delegate Inheritance

- `URLSessionDelegate`
  - `URLSessionTaskDelegate`
    - `URLSessionDataDelagate`
    - `URLSessionDownloadDelagate`

### Delegate 지정

```swift
var session: URLSession!

func sendRequest() {
  guard let url = URL(string: /** URL String */) else { return }

  let configuration = URLSessionConfiguration.default

  session = URLSession(configuration: configuration, delegate: self, delegateQueue: OperationQueue.main)

  let task = session.dataTask(with: url)
  task.resume()
}
```

- session과 viewController 객체가 강한 참조로 연결되어 있음
  이렇게 session 생성자로 delegate 지정 시, 반드시 통신이 완료하고 나서 session을 정리해주어야 메모리 누수가 발생하지 않음

```swift
// Or deinit method
override func viewWillDisappear(_ animated: Bool) {
  super.viewWillDisappear(animated)

  session.finishTasksAndInvalidate()
  session.invalidateAndCancel()
}
```

- `finishTasksAndInvalidate()`: 모든 통신이 완료되면 session 객체를 invalidate 시킴
- `invalidateAndCancel()`: 통신 완료 여부와 상관 없이 취소 후 invalidate 시킴

### Delegate Methods

```swift
extension ViewController: URLSessionDataDelegate {
  func urlSession(_ session: URLSession, dataTask: URLSessionDataTask, didRecieve response: URLResponse, completionHandler: @escaping (URLSession.ResponseDisposition) -> Void) {}

  func urlSession(_ session: URLSession, dataTask: URLSessionDataTask, didRecieve data: Data) {}

  func urlSession(_ session: URLSession, task: URLSessionTask, didCompleteWithError error: Error?) {}
}
```

- dataTask를 이용시, `URLSessionDataDelegate` 프로토콜을 채용
- `urlSession(_ session:, dataTask:, didRecieve:, completionHandler:)`: 서버로부터 최초로 응답을 받았을 때 호출됨
- `urlSession(_ session:, dataTask:, didRecieve)`: 서버로부터 데이터가 전송될 때 마다 호출됨. 파라미터로 들어오는 데이터는 전체 데이터가 아니라 부분 데이터이기 때문에, 호출되는 시점마다 데이터를 누적시킨 이후 완료되면 파싱하는 방식으로 이용
- `urlSession(_ session:, task:, didCompleteWithError)`: 서버로부터 데이터가 전송 완료되는 시점에 호출됨
