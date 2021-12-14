## URL Loading System

### URLSession

- URL Loading System에서 가장 기초적이자 중요한 객체
- 네트워크 연결 설정, 요청과 응답을 처리
- `URL Session Configuration`을 통해 네트워크 연결과 관련된 것들을 설정할 수 있음

  <br/>

- **Shared Session**

  - 단순한 네트워크 요청
  - 백그라운드 전송 지원 X

- **Default Session**

  - 세션을 직접 구현할 때 사용
  - Shared Session을 쓰는 일은 거의 없고, 대부분 Default Session으로 구현
  - 기본 캐싱 처리 지원(디스크 + 메모리)

- **Ephemeral Session**

  - Default Session과 같지만, 어떠한 데이터도 디스크에 저장하지 않고 메모리에만 저장함
  - URLSession이 invalid 되는 시점에 데이터가 모두 사라지기 때문에 데이터 유출 위험이 상당히 낮음
  - 프라이빗 브라우징 등의 기능을 구현할 때 사용

- **Background Session**

  - 앱 실행 상태와 관계없이 파일을 업로드하고 다운로드할 때 사용

### Task

- 세션을 생성한 이후 task를 생성
- URLSession을 통해 전달하는 개별 요청을 task라고 함

> Task는 Pending 상태로 반환되기 때문에 반드시 `resume()`메소드를 호출해주어야 함

- **Data Task**

  - API 서버와 통신 시에 생성하는 기본 task

- **Upload / Download Task**

  - 파일 전송을 구현할 때 사용
  - 백그라운드 전송 지원

- **Stream Taskn**

  - 채팅과 같은 TCP 통신 개발 시 적합

### URLRequest

- POST와 같은 방식의 통신을 할 때, Body로 데이터를 전달해야 할 때 사용

```swift
var request = URLRequest(url: url)
request.addValue("application/json", forHTTPHeaderField: "Content-Type")
request.httpMethod = "POST"
request.httpBody = /** body data */

let task = URLSession.shared.dataTask(with: request) { /** ... */}
task.resume()
```

### Response Handling

- **Completion Handler**

  - 테스크가 종료되는 시점에 한 번만 호출
  - 서버에서 전달된 데이터는 Completion Handler로 한 번에 전달됨

- **Session Delegate**
  - 테스트가 진행되는 동안 다양한 이벤트를 처리하고 싶을 때 적합

> Completion Handler와 Session Delegate는 동시에 구현할 수 없음
