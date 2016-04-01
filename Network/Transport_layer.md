## Transport Layer

### 트랜스포트 레이어의 기본 동작원리

### transport services and protocols

- logical end-end transport
- 어플리케이션 레이어에서 내려온 데이터의 크기가 너무 클 경우 segments라는 단위로 쪼개줌
- segment 단위로 전송
- 상대편 transport layer에서는 segment단위로 받은 데이터를 다시 복원한 후에 application layer로 올려보내줌
- household analogy(편지에 비유)
- network layer에서는 집에서 집까지만 보내주고, 집 안에서 누가(어떤 프로세스가) 받을지는 transport layer에서 처리해준다.

### Internet transport-layer protocols

- reliable, in-order delivery(TCP)
- unreliable, unordered delivery(UDP)

### Multiplexing / demultiplexing

- multiplexing : 두개 이상의 application 소켓에서부터 전달받은 데이터를 각각 segment단위로 만들어서, 어느쪽에서 왔는지 여부와 관계없이 네트워크 레이어로 전달해줌(우체부 가방 안의 편지들)
- 네트워크 레이어에서는 이렇게 받은 세그먼트 단위의 정보에dest IP addr, source IP addr, port number 등을 추가해서 보내줌
- application layer에서 코딩할때 목적지주소와 port번호를 쓰는 이유!(source IP addr은 제공되는 메소드에서 자동으로 붙여주는듯)
- TCP socket identified by 4-tuple : source IP addr, dest IP addr, source portNum, dest portNum
- ex) 웹상에서 데이터를 주고받을떄 dest IP addr와 dest PortNum만 가지고는 여러개의 요청을 처리해줄 수 없기 때문에 source의 IP와 portnumber도 참고해서 데이터를 전달하게 됨

### connectionless

- UDP
- no handshaking
- 각각의 segment가 독립적으로 처리됨
- 패킷 손실이 있을 수 있고
- 순서가 뒤바뀔수도 있다
- 많이 쓰는 분야 : streaming multimedia apps, DNS, SNMP등
- reliable transfer over UDP : UDP 방식을 사용하면 데이터의 손실이 일어날 수 있지만, 이를 보완하는 방법으로 어플리케이션 레이어 상에서 처리를 해서 데이터 손실을 막는 방법도 있음
- UDP를 사용하는 이유 : no connection establishment, simple, small header size, no congestion control등의 이유때문(간결, 신속)

### UDP checksum

- 전달 과정에서 에러(비트가 바뀌는 현상)이 있는지 확인
- 세그먼트를 16비트 단위로 쪼개고, 각각을 수로 인식해서 다 더해주고 비트를 뒤집음 (sum + checksum = 0)
- 받는쪽에서도 checksum을 확인해서 둘이 다르면 에러가 발생, 둘이 같으면 에러가 아닐 확률이 높음
- checksum -> error판단 
- UDP의 headersize : 8bite(작다)

### Principles of reliable data transfer

- network layer에서 제공하는 서비스는 unreliable layer임..
- 어떻게 하면 transport layer에서 데이터의 손실, 변형등이 없이 전송할 수 있을까
- network layer에서 unreliable 수준도 다름

#### rdt 1.0 (아래 채널에서 패킷의 손실이 전혀 없다고 가정했을때) application layer에서는 패킷을 만들어서 보내기만 하면됨
- rdt_send(data), rdt_rcv(packet)

#### rdt 2.0 (아래 채널에서 비트 에러가 발생할 수 있는 경우)
- 수신한 쪽에서 checksum을 확인해보고, 정상적일때는 ok사인을(acknowledgements, ACKs), 비정상적일때는 no 사인을(negative acknoledgements, NACKs) 보냄
- 발신한 쪽에서는 패킷을 보내고, 응답을 기다림.. 응답이 어떻게 오는지에 따라서 다음 데이터를 보내거나 다시 보내거나
- ACK or NAK를 돌려보냈는데, 이 과정에서 데이터에 손실이 발생한다면?... 재전송해야됨(sequence number를 통해서 구분해줌)
- 이런 프로토콜을 Stop and wait 방식이라고 함

#### rdt2.1 : sender, handles garbled ACK/NAKs

#### rdt3.0 : channels with errors and loss

- 정상적인 경우라도, stop and wait 알고리즘을 사용하게 되면, 회선의 사용률이 많이 떨어지게 된다... 성능 이슈 발생

### 이러한 문제를 보완하기 위해서... Pipelined protocols

- 패킷에 대한 응답을 받기 전에 미리 여러개의 data 패킷을 보냄
- ACK packet 여러개를 받기 위한 버퍼를 마련
- ex) 3개의 패킷을 동시에 다루는 경우... 세개의 패킷을 보내고, 첫번쨰 응답이 오는 시점에 바로 하나의 패킷을 추가로 보냄

#### Go-back-N

- 순서대로 보내고, 순서대로 받은데까지만 받았다고 처리하고, 중간에 패킷 하나가 빠진다면 그 뒤에 오는것들은 전부 무시하고 받은데부터 다시 패킷을 보내는 방식
- 장점 : ACK가 몇개 사라져도 안정적으로 동작
- 단점 : 실제로 뒤에 도착한 패킷들도 가운데 뭐 하나만 빠지면 전부 무시하기 때문에 낭비발생 
- Time out은 가장 오래전에 보낸 패킷을 기준으로 하나만 동작


#### Selective Repeat

- Go-back-N이 맨 앞의 패킷만 timer사용하는데 반해서, 각각의 패킷에 대해서 timer를 적용해서 처리(out of order packet을 담기 위해 buffer 마련)
- window size는 맨 앞의 패킷을 기준으로 설정
- window size가 정해지면, sequence number의 개수를 정할 수 있음(sender's window size + receiver's windowsize <= sequence number)
- TCP congestion : window size를 조절해서 속도 조절
- TCP congestion과 flow controll을 고려해서 window size를 통해 속도를 조절

#### TCP sequence numbers, ACKs

