## __Router__
---
### __Router (라우터)__
+ 서로 다른 Network를 연결하고 Broadcast Domain영역을 나눈다.
+ 3계층 (Network Layer) 장비
+ 특정 interface를 통하여 수신한 packet의 목적지 주소를 보고 목적지와 연결된 interface를 통해 전송한다.
  
<br>

### __Router의 기능__
1. 경로 결정 : 목적지까지 가는 경로를 확인하고 어느 경로가 가장 최적의 경로인지 파악하고 결정 (Routing)
2. 스위칭 : 결정된 경로대로 packet을 전송
3. Routing Table : 최적의 경로가 저장되어 있는 테이블로 이를 이용하여 packet을 전송한다.
4. Routing Protocol : 최적의 경로를 찾는 학습 능력을 가지고 있으며 이를 이용해 라우팅 테이블을 작성. 또한 각 프로토콜마다 길이가 다르므로 선택해서 사용
5. 목적지까지 전송을 책임지지 않고 경로 상의 다음 라우터한테 전송만 한다.

<br>

### __Router의 종류__
1. 단독형 : 일체형으로 이미 모든 인터페이스가 구비되어 있는 형태로 확장하기에 용이하지 않다.
2. 모듈형 : 필요에 따라 인터페이스를 직접 꽂아서 사용할 수 있는 형태로 확장성이 용이하다.
<br>

### __Router Interface의 종류__
1. LAN 구간 Interface : Ethernet (Fast Ethernet) Interface
2. WAN 구간 Interface : Serial Interface
3. 관리용 Interface : Console Port

<br>

### __Router의 Mode__
1. User Mode
   - 라우터의 현재 상태만 확인 가능
   - 라우터의 기본 시작 형태
   - 형태 : Router >
  
2. Privilege Mode
   - User Mode에서 enable(en)을 입력하면 Privilege Mode로 변환 가능
   - 라우터의 설정을 확인하거나 연결 테스트 진행 가능
   - BUT, 설정 변경은 불가능
   - 형태 : Router #
  
3. Global Configuration Mode
   - Privilege Mode에서 configure terminal(conf t) 입력하면 Global Configuration Mode로 변환 가능
   - 라우터의 설정 진행 가능
   - 형태 : Router(config) #

<br>

### __추가 TIP__
+ 라우터의 단계는 User Mode부터 한 단계씩 차근차근 올라야 한다. 따라서 User -> Global단계로 바로 올라가는 것은 불가능
+ exit : 전 단계로 이동
+ ? : 해당 명령어에 대한 설명 보여줌
+ tab 키 : 자동 완성 기능 (단, 해당 철자에 대한 명령어가 1개일 경우에만 자동 완성 가능)