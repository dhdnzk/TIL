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

#### NAT : network address translation

    - 라우터에 대표 IP주소 하나만 부여받고, 내부 네트워크에서 새로운 ip를 할당함.

    - 내부에서 외부로 패킷을 보내지 않는 이상, 외부에서 내부의 로컬네트워크상의 ip주소로 패킷을 보내는것은 불가능(보안!)

    - NAT를 사용하면 60000개의 엔터티를 커버할 수 있음.
    
    - P2P 연결요청을 할때 NAT Router에 의해서 막혀버리는 경우가 생김

#### Traceroute and ICMP

    - ICMP를 이용해서 출발지부터 목적지까지의 경로를 탐색함

    - TTL을 1로 설정해서 세번 보내고, 2로 설정해서 세번 보내고... 목적지에 도착할때까지 반복

    - 잘 사용되지 않을법한 포트번호를 붙여서 보내줌

    - 목적지에 도착하면 포트넘버에 해당하는 프로세스가 없으므로 (type3, code3)에러를 반환함

    - 이때 반환하는 패킷을 보고 출발지에서 도착했는지를 판단


### IPv6

#### IPv6 datagram format

#### Transition from IPv4 to IPv6

    - no flag days... IPv4와 IPv6가 섞여있는 상황에서도 잘 작동하게 하기 위해서 tunneling 기법을 사용.

    - tunneling : IPv4 패킷의 pay load에 해당하는 부분에 IPv6 패킷을 통째로 삽입... 

    - 라우터에서 터널링 프로토콜을 만들어서(IPv4포맷으로) 보내고, 라우터에서 해석해서 IPv6으로 다시 변환

    - a 
