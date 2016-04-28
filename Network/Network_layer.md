## Network Layer

- transport segment를 받고 이를 데이터부분에 저장, IP주소를 받아서 패킷으로 만듬
- transport segment랑 IP address만 알면됨
- application layer와 transport layer는 host network에만 있고, network layer는 모든 라우터에 존재

### routing & forwarding

- routing : 근처 라우터들과 정보를 주고받는 프로세스를 두고, 이를 통해서 필요한 경로상의 네트워크 구조를 파악

- forwarding : 만들어진 라우팅 테이블을 참조해서 패킷이 들어왔을때 어느쪽으로 보내줄지 결정
- routing & forwarding이 협업

### virtual circuites

- host부터 목적지 host까지 하나의 선으로 연결되어 있는것처럼 
- virtual circuit 
- VC forwarding table

### Datagram network

- 주변 네트워크 연결 상황을 파악할 필요 없이 (flow 신경안쓰고) 인접한 라우터에 관한 table만 참고해서 패킷 전달
- 인터넷은 datagram network를 사용

### Router architecture overview

### IP addressing

- 랜카드에(interface에) IP address를 부여
- subnet
- CIDR (Classless InterDomain Routing)
- DHCP (Dynamic Host Configuration Protocol)

