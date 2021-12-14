## HTTP와 HTTPS

### HTTP

HyperText Transfer Protocol
웹 상에서 클라이언트와 서버가 서로 정보를 주고 받을 수 있도록 하는 통신 규약(프로토콜)
일반적인 plain text로 통신하기 때문에 보안에 취약함

### HTTPS

HyperText Transfer Protocol over Secure Socket Layer, HTTP over TLS, HTTP over SSL, HTTP Secure
HTTP의 일반 텍스트에 SSL이나 TLS 프로토콜을 씌워 데이터를 암호화하는 기법

### HTTPS 장점

- **보안성**

  - **SSL 인증서**를 이용하여 데이터를 암호화

- **SEO 품질**
  - 구글과 같은 포털 사이트에서도 HTTPS 사이트에 가산점을 부여
  - 실제로 방문자들도 안전하다고 여겨지는 사이트를 더 방문하는 경향

### TLS(Transport Layer Security, 전송 계층 보안)

컴퓨터 네트워크에 통신 보안을 제공하기 위해 설계된 암호 규약
TLS는 가장 최신 기술로 강력한 버전의 SSL
여전히 보안 인증서는 SSL이라고 불려짐

- TCP/IP 네트워크를 사용하는 통신에 적용됨
- 통신 과정에서 전송계층의 종단간 보안과 데이터 무결성을 보장

- TLS 3단계 과정
  1. 지원 가능한 알고리즘을 서로 교환
  2. 키 교환 및 인증
  3. 대칭키 암호로 암호화 하고 메세지 인증

TLS(전송 계층 보안) 프로토콜을 통해서도 보안을 유지합니다. TSL은 데이터 무결성을 제공하기 때문에 데이터가 전송 중에 수정되거나 손상되는 것을 방지하고, 사용자가 자신이 의도하는 웹사이트와 통신하고 있음을 입증하는 인증 기능도 제공하고 있습니다

### HTTPS 통신 과정

![Screen Shot 2021-12-13 at 2 27 04 PM](https://user-images.githubusercontent.com/38246878/145757280-0a049fb3-597c-42c3-928c-2124185e0248.png)

1. **서버**: 한쌍의 공개키와 개인키를 생성함. 사이트의 각종 정보와 공개키를 인증기관에 전달하여 SSL 인증서 생성 요청
2. **인증기관(CA)**: SSL 인증서 발급. 인증기관은 자신만의 공개키와 개인키 한쌍을 생성. SSL 인증서를 자신의 개인키로 암호화하여 서버로 전달하고 서버는 이 인증서를 게시함
3. **브라우저**: 인증기관의 개인키로 암호화된 SSL 인증서를 전달받음.
4. **브라우저**: 인증기관에서 공개하고 있는 인증기관의 공개키를 가져와 이 SSL 인증서를 복호화. 이 인증서를 보유한 웹 서버가 진짜임을 밝히고 발급한 대상이 인증기관임을 알게됨. 동시에 서버의 공개키를 확보.
5. **브라우저/서버**: 웹 브라우저가 서버를 신뢰함. 방금 전달받은 공개키로 실제 데이터 암호화에 사용할 비밀키(대칭키)를 암호화하여 서버에 전달.
6. **서버**: 서버는 브라우저가 자신(서버)의 공개키로 암호화하여 전달한 비밀키를 자신의 개인키로 복호화. 이로써 서버와 브라우저는 동일한 비밀키(대칭키)를 보유하게 됨.