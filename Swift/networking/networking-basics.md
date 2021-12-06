## Networking Basics

iOS에서 권장하는 네트워크 규칙

1. High-Level API 사용
2. 필요한 양 만큼의 데이터만 통신
3. Caching + Cancellable
4. Asynchronous API 사용

- 메인스레드를 블록하면 안됨
- Sync API 사용 시, 반드시 백그라운드 스레드에서 실행

5. Hostnames 사용
6. HTTPS 사용 (IPv6 사용)

### URLSession

> NSURLConnection은 Deprecated 되고 전부 URLSession으로 대체됨

API Request, 파일 전송, Authentication 등에 사용

### Webkit

> UIWebView가 아닌, WKWebView를 사용할 것

Web 콘텐츠를 표시하고, 브라우징 기능을 제공함. 자바스크립트를 컨트롤할 수 있음

### Network

> iOS12 부터 가능한 API. 소켓 통신에 활용할 수 있는 API 제공.

TLS, TCP, UDP 통신에 활용
