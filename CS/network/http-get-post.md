## HTTP의 GET과 POST

### 통신 프로토콜

통신 프로토콜(통신 규약)은 컴퓨터나 원거리 통신 장비 사이에서 메세지를 주고 받는 양식과 규칙. 신호 체계, 인증, 오류 감지 및 수정 기능 등을 포함함

- **HTTP**: Hyper Text Transfer Protocol
- **HTTPS**: Hyper Text Transfer Protocol Secure
- **FTP**: File Transfer Protocol
- **SFTP**: Secure File Transfer Protocol
- **Telnet**: TErminaL NETwork
- **SMTP**: Simple Mail Transfer Protocol
- **SSH**: Secure Shell
- **SSL**: Secure Socket Layer

### HTTP 프로토콜

HTTP(HyperText Transfer Protocol)은 웹 상에서 정보를 주고받을 수 있는 통신 규약.

- 클라이언트와 서버 사이에 이루어지는 요청(Request)/응답(Response) 프로토콜
- HTTP를 통해 전달되는 자료는 http:로 시작되는 URL로 조회할 수 있음
- 주로 HTML 문서를 주고 받는데에 쓰임
- 주로 TCP 방식을 사용하고, HTTP/3부터는 UDP를 사용하며 80번 포트를 이용함

> 클라이언트와 서버 사이의 소통은 평문(ASCII) 메세지로 이루어짐. 클라이언트는 서버로 요청 메세지를 전달하며 서버는 응답메세지를 보냄.

### GET 방식

GET 방식은 요청하는 데이터가 HTTP Request Message의 Header 부분에 url이 담겨서 전송됨. 그래서 `url?{key}={value}`방식으로 전송(아무것도 넣지 않으면, BODY가 빈 상태로 보내짐)

- url에 담겨서 보내지므로, 보낼 수 있는 데이터의 크기가 제한적
- 보안이 필요한 데이터에 대해서 url에 그대로 노출되므로 GET방식은 적절하지 않음

### POST 방식

POST 방식은 HTTP Request Message의 Body 부분에 데이터가 담겨서 전송됨. 바이너리 데이터를 요청할 때 처럼 데이터의 크기가 크거나 보안성이 중요할 때 POST 방식을 사용(암호화 처리를 필수적으로 진행해야 함)

- Content-Type이라는 Header 필드가 들어가서 어떤 데이터 타입인지 명시함. POST 방식으로 데이터를 보낼 때는 Content-Type를 통해 콘텐츠 타입을 꼭 명시해주어야 함.

### 차이점

- GET은 가져오는 것(QUERY), POST는 서버의 값이나 상태를 변경하거나 추가하기 위해 사용(MUTATION)
- GET 방식은 브라우저 상에서 Caching 처리가 가능함. 따라서 GET 방식의 통신 시에, 캐싱된 데이터가 응답될 가능성이 존재함(캐싱 처리 덕분에 속도 면에서는 GET 방식이 빠름)
