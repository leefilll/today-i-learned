## TCP/IP 모델

OSI 7계층에서 4계층으로 바꾼 것이라 생각하면 쉬움.

### TCP와 IP

TCP/IP는 패킷 통신 방식의 IP(Internet Protocol, 인터넷 프로토콜)와 전송 조절 프로토콜인 TCP(Transmission Control Protocol, 전송제어 프로토콜)로 이루어짐. HTTP, FTP, SMTP 등 TCP를 기반으로 한 수많은 애플리케이션 프로토콜이 IP위에서 동작하기 때문에 TCP/IP로 부름.

- **TCP**
  근거리 통신망이나 인트라넷, 인터넷에 연결된 컴퓨터에서 실행되는 프로그램 간에 일련의 바이트를 안정적으로, 순서대로 교환할 수 있게 해줌.
  웹 브라우저들이 서버에 연결할 때 사용하거나 이메일 전송이나 파일 전송에도 사용.

- **IP**
  송신 호스트와 수신 호스트가 패킷 교환 네트워크에서 정보를 주고받는 데 사용하는데 사용하는 프로토콜. IP의 정보는 패킷 혹은 데이터그램이라고 하는 덩어리로 나뉘어 전송됨. 비신뢰성(보낸 정보에 대해서 보장하지 않음)과 비연결성이 특징.
  현재 IPv4가 표준 프로토콜이나, 주소공간 고갈 문제로 인해서 IPv6가 대중화되고 잇음.

### TCP/IP 모델과 OSI 모델

- 두 모델은 관련은 있으나, 완전히 들어맞지는 않음.
- OSI 모델이 더 잘 맞는 경우는 SSL이나 TLS인 경우

<img width="1312" alt="tpc-ip-and-osi-model-cellbiol com_" src="https://user-images.githubusercontent.com/38246878/144557829-eb2486f7-73f4-48a7-b538-ab15188aafe3.png">
