## URL Session Configuration

`URLSessionConfiguration` 객체는 네트워크 연결과 관련된 속성을 설정

- 네트워크 타입(Cellular Usage 등)
- 쿠키/캐시 정책
- 저장소
- Timeout

`URLSessionConfiguration`은 `URLSession` 생성 이전에 항상 초기화를 완료 해야함. 그리고 `URLSession`의 생성자로 전달. 같은 `URLSession`을 통해 생성된 모든 task는 동일한 설정을 공유하고, 생성 이후에는 설정 값을 변경할 수 없음

### Configuration Types

- **Shared Session Configuration**
  시스템에서 사용하는 기본 설정

  ```swift
  let session = URLSession.shared
  ```

- **Default Session Configuration**
  Session Delegate와 Caching이 포함된 기본 설정
  인증 정보 같은 민감한 정보는 키체인에 저장하고, 나머지는 디스크에 저장됨

  ```swift
  let configuration = URLSessionConfiguration.default
  let session = URLSession(configuration: configuration)
  ```

- **Ephemeral Session Configuration**
  Session Delegate와 Caching이 포함되었지만, 메모리에만 캐싱을 저장하는 것이 다름
  인증 정보 또한 메모리에 저장
  URLSession을 invalidate하면, 모든 캐시가 사라짐

  ```swift
  let configuration = URLSessionConfiguration.ephemeral
  let session = URLSession(configuration: configuration)
  ```

- **Background Session Configuration**
  Session Delegate와 Background 전송이 지원됨

  ```swift
  let configuration = URLSessionConfiguration.background(withIdentifier: "Identifier")
  let session = URLSession(configuration: configuration)
  ```

- **Custom Session Configuration**

  ```swift
  let configuration = URLSessionConfiguration.default
  configuration.timeoutIntervalForRequest = 30
  configuration.httpAdditionalHeaders = ["API-VERSION": "1.1.2"]
  configuration.networkServiceType = .responseData
  let session = URLSession(configuration: configuration)
  ```
