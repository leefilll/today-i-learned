## Caching

네트워크 응답은 항상 고비용의 작업이고, 서버의 리소스를 사용하기 때문에 불필요한 트래픽을 최소화하여야 함. 따라서 네트워크 프로그래밍에서 캐싱은 필수. iOS에서는 서버에서 전달된 데이터를 디스크와 메모리에 저장함.

- Cache Store: 기본적으로 제공되는 캐시 저장소. 그대로 사용하는 것도 가능
- Cache Policy: 캐시 정책에 따라서 캐시 사용 방식이 정해짐

### Cache Policy

- **useProtocolCachePolicy**

  - 가장 기본 정책
  - 서버에서 설정한 `Cache-Control` 헤더에 따라서 동작함
  - 가장 단순한 구현
    <br/>

- **reloadIgnoringLocalCacheData**

  - 로컬 캐시를 아예 무시함
  - 매번 네트워크에 연결하는 과정이 수반됨
  - 주로 영구 정책으로는 사용하지 않고, 특정 요청에 대해서 캐시를 갱신할 때 임의로 사용함
    <br/>

- **returnCacheDataDontLoad**

  - 항상 로컬 캐시를 사용함
  - 로컬 캐시가 존재하지 않는다면, 요청에 실패함
  - 항상 서버에서 전달되는 데이터가 동일할 때 사용하면 좋음
    <br/>

- **returnCacheDataElseLoad**

  - 캐시가 저장되어 있는 지 확인하고, 없다면 네트워크에 요청함
    <br/>

### URLCache

만료된 캐시는 직접 삭제해주어야 함. 이를 위한 메소드는 `URLCache` 클래스에 선언되어 있음

```swift
session.configuration.urlCache?.removeAllCachedResponsed()
```
