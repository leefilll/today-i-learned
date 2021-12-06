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
