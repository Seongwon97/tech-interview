# 네트워크
## TCP & UDP
<details>
<summary>TCP와 UDP의 차이점에 대해 설명해주세요.</summary>

<br>

- TCP는 Receiver와 Sender사이에 연결을 만들고 해당 연결을 기반으로 데이터를 주고받는 **연결 지향형 프로토콜**이며 UDP는 연결 없이 전송하는 **비연결형 프로토콜**이다.
- TCP는 데이터를 순서대로 보내고 순서대로 수신하는 반면에 UDP는 수신의 순서가 중요하지 않다.
- TCP는 연결의 체증을 제어하기 위해 흐름제어(Flow Control)과 혼잡제어(Congestion Control)을 진행한다. 반대로 UDP는 수행하지 않는다.
- 속도 측면에서는 비연결형인 UDP가 더 빨라서 스트리밍과 같이 연속성이 중요한 서비스에 사용된다. 반면에 TCP는 속도가 느린대신 연결을 맺고 통신을 하기에 신뢰성이 중요한 서비스에 이용한다.

![](img/network/img.png)

</details>


<details>
<summary>DNS와 DHCP는 UDP와 TCP중 어떤 프로토콜을 사용할까요?</summary>

<br>

- UDP를 사용한다. 그 이유는 Sender, Receiver사이에 연결을 맺으면 보내고 받는 데이터 크기에 비하여 연결에 드는 비용이 더 크기 때문이다. Root DNS 같은 경우 모든 것들과 TCP로 연결을 맺게 된다면 부담이 너무 크기에 연결 없는 UDP방식을 사용한다.

</details>


<details>
<summary>UDP, TCP의 세그먼트(Segment)는 전송 과정 중 데이터의 변경이 없었다는 것을 어떻게 알까요?</summary>

<br>

각각의 세그먼트는 헤더의 Checksum을 통해 데이터의 변경이 발생했는지 체크를 해준다.

- Sender는 세그먼트의 16-bit로 표현한 Content와 Header필드 값을 더한 다음 1의 보수를 만들어 checksum 필드에 추가한다.
- Receiver는 반대로 Content와 Header의 필드값을 16-bit로 변환 후 더한 값을 1의 보수로 변경한 후 checksum의 필드와 같은지 확인한다. 만약 같다면 데이터 전송 과정에서 문제가 발생하지 않은 것이고, 다르다면 해당 세그먼드는 에러가 담긴 세그먼트로 판단한다.

</details>


<details>
<summary>TCP 3 way handshake에 대해서 설명해주세요.</summary>

<br>

3 way handshake는 TCP통신에서 가상회선을 만드는 단계이다. 회선을 만드는 과정에서는 SYN 패킷과 ACK 패킷을 통해 회선을 만든다. 과정은 아래와 같다.

1. 클라이언트는 서버에 접속을 요청하는 SYN 패킷을 보낸다.
2. 서버는 SYN요청을 받고 클라이언트에게 요청을 수락한다는 ACK 와 SYN flag 가 설정된 패킷을 발송하고 클라이언트가 다시 ACK으로 응답하기를 기다린다.
3. 클라이언트는 서버에게 연결을 맺었다는 ACK을 보내고 이후로부터는 연결이 이루어지게 된다.

</details>


<details>
<summary>TCP 4 way handshake에 대해서 설명해주세요.</summary>

<br>

4 way handshake는 TCP통신에서 가상 회선을 해제하는 단계이다. 과정은 아래와 같다.

1. 클라이언트가 연결을 종료하겠다는 FIN플래그를 전송한다.
2. 서버는 확인메시지(ACK)를 보내고 자신의 통신이 끝날때까지 기다리는 `TIME_WAIT`상태가 된다.
3. 서버가 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN플래그를 전송한다.
4. 클라이언트는 확인했다는 메시지를 보낸다.

</details>


<details>
<summary>왜 연결을 끊을 때는 4way handshke를 할까요?</summary>

<br>

- Client가 데이터 전송을 마쳐서 연결을 끊으려 하더라도 Server는 아직 보낼 데이터가 남아 있을 수 있기 때문에 일단 FIN에 대한 ACK만 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메세지를 보낸다.

</details>


<details>
<summary>Time-out이란 무엇일까요?</summary>

<br>

4way handshake에서 Server에서 FIN을 전송하기 전에 전송한 패킷이 Routing 지연이나 패킷 유실로 인한 재전송 등으로 인해 FIN패킷보다 늦게 도착하는 상황이 발생하면 해당 패킷은 Drop되고 데이터는 유실될 것이다. 이러한 현상에 대비하여 Client는 Server로부터 FIN을 수신하더라도 일정시간(디폴트 240초) 동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을 거치게 되는데 이 과정을 TIME_WAIT 라고 한다.

</details>


<details>
<summary>TCP와 UDP 패킷구조에는 어떤 차이가 있을까요?</summary>

<br>

UDP는 비연결형 통신이라 출발지와 목적지의 Port정보와 UDP 세그먼트의 길이, checksum, data(payload)만을 갖고 있다.

하지만 TCP는 연결형 통신에 데이터간 전송 순서를 보장해야하기에 sequence number, ack number, receive window등 여러 추가 데이터들이 들어간다.

</details>
