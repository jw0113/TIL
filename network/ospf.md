## __OSPF__
---
### __OSPF__
+ Link-State 라우팅 프로토콜
+ Classless 라우팅 프로토콜
+ Metric : cost
+ AD값 : 110
+ Multicast 사용해서 정보를 전달한다.
+ SPF or Dijkstra 알고리즘을 통해 최적 경로 계산
+ OSPF Area 존재한다.

1. 장점
   - Area단위로 구성하고 있어 대규모 네트워크에 안정적으로 운영 가능
   - 특정 area정보를 다른 area에 전송하지 않으므로 안전
   - Stub이라는 강력한 축약 기능이 있어 Routing table크기를 획기적으로 줄일 수 있다.
   - 표준 Routing Protocol
   - Convergence Time이 빠른 편

2. 단점
   - 설정 복잡 (네트워크에 따라 동작 방식이 다르기 때문)
   - 라우팅 정보 계산 및 유지를 위해 하드웨어 장비 지원이 필요하다.

<br><br>

### __OSPF 동작 방식과 Packet__
1. OSPF를 설정한 Router끼리 Hello Packet을 주고 받으며 Neighbor or adjancent Neighbor을 맺는다.
2. LSA들을 교환하며 전송 받은 LSA를 Link-State Database에 저장<br>
   1) DBD Packet : LSA들의 요약된(간략하게) 정보를 넣어서 보내며 알려준다.
   2) LSR Packet : Neighbor에게서 수신한 LSA에서 모르는 정보가 있을 경우 상세 정보를 요청할 때 사용한다.
   3) LSU Packet : LSR의 답장이나 네트워크가 변했을 때 알려주기 위해 사용한다.
   4) LSAck Packet : DBD, LSR, LSU일 경우 Packet을 정상적으로 수신했음을 알려줄 때 사용한다.
3. LSA를 모두 교환하고 SPF of Dijkstra 알고리즘을 이용하여 최적 경로 계산 후 Routing table에 올린다.
4. 그 후에도 주기적으로 Hello Packet을 교환하면서 정상 동작을 확인한다.
5. 네트워크 상태가 변하면 위의 과정을 다시 반복하면서 Routing table을 생성한다.

<br><br>

### __OSPF Neighbor State__
1. Down 상태 : OSPF가 설정되고 Hello Packet을 전송했지만 상대방 Hello Packet을 받지 못한 상태
2. Init 상태 : 상대방 Hello Packet을 받았지만 아직 상대방이 내가 보낸 Hello Packet을 받지 못한 상태
3. Two-way 상태 : Neighbor와 쌍방향 통신이 이루어진 상태
4. Exstart 상태 : adjacent Neighbor이 되는 첫번째 단계, Master & Slave Router을 선출한다.
5. Exchange 상태 : 각 Router가 자신의 Link-State Database에 저장된 LSA의 Header만을 DBD Packet에 담아 상대방에 전송한 상태
6. Loading 상태 : DBD Packet 교환 후 자신에게 없는 정보를 LSR Packet으로 요청하고 LSU를 받는 상태
7. Full 상태 : 라우팅 정보 교환이 모두 끝난 상태

<br><br>

### __네트워크 타입 (종류에 따라 OSPF 연결 형태가 다르다.)__
1. Broadcast Multi Access
   + Broadcast (동일 네트워크 안 모든 장비에게 전송하는 네트워크) + Multi Access (하나의 인터페이스를 통해 다수의 장비와 연결한 네트워크)
   + 하나의 Packet만 전송해 모든 장비에 전송되는 형태
2. Non Broadcast Multi Access (NBMA)
   + Broadcast가 지원되지 않은 Multi Access 네트워크
   + 내부의 Virtual Circuit (가상회로 = 가상 인터페이스) 방식을 사용한다.
   + 모든 장비에 전송해야 하는 경우 가상회로 하나당 하나의 Packet을 전송하는 방식
3. Point-to-Point (1:1방식)
   + 하나의 인터페이스에 연결된 장비가 하나뿐인 형태

<br><br>

### __DR/BDR__
+ Multi Access일 경우 중복된 정보를 계속 교환하는 문제점이 발생한다. 이를 방지하기 위해 DR/BDR을 선출한다.
+ DR : 중계역할을 담당하는 대표자. 모든 라우터는 DR이랑만 정보를 교환한다.
+ BDR : DR에 문제가 생겼을 경우 DR역할을 대신 할 부대표 역할.
+ Multi Access 네트워크에서만 사용한다.

<br><br>

### __DR 선출 방법__
1순위) OSPF Priority가 가장 높은 Router<br>
2순위) Router ID가 높은 Router <br>
3순위) Loopback 주소로 판단
+ DR/BDR이 선출된 후 더 높은 순위의 Router가 추가되어도 변경되진 않는다.
+ DR이 다운될 경우 BDR이 DR이 되고 새로 BDR을 뽑는다.
+ DR/BDR이 아닌 나머지 Router은 DROTHER이라고 한다.
<br><br>

### __OSPF Area__
+ Area가 여러개일 경우 하나는 반드시 Area 0으로 설정한다.
+ Area 0은 backbone Area로 다른 Area들과 물리적으로 연결되어 있어야 한다.

<br><br>

### __OSPF Router 종류__
1. Backbone Router : Backbone Area (= 0)에 속한 Router
2. Internal Router : 하나의 Area에 속한 Router
3. ABR (Area Border Router) : 두 개 이상의 Area에 소속된 경계 Router
4. ASBR (AS Boundary Router) : 서로 다른 Routing Protocol이 설정된 네트워크를 연결하는 AS 경계 Router

<br><br>

### __OSPF 설정 방법__
```
router(conifg) # router ospf 프로세스ID
router(conifg-router) # network 네트워크ID wildcard mask area *
```
+ show ip route를 통해 설정 확인한다.

<br><br>

### __Loopback Interface 설정 방법__
```
router(conifg) # interface loopback 루프백인터페이스 번호
router(conifg) # ip address IP주소 subnet mask
router(conifg) # no shutdown
```

<br>

### __DR/BDR 설정 초기화하는 방법__
```
router(conifg) # clear ip ospf process
```
<br>

### __backbone Area와 다른 Area를 연결하는 방법__
```
router(conifg) # router ospf 1
router(conifg) # network IP주소 wildcard mask area *
```
+ 각 시리얼 인터페이스가 어느 Area에 속하는지 보고 맞는 Area를 설정해준다.

<br><br>

### __Redistribute (재분배)__
+ 재분배는 서로 다른 라우팅 프로토콜을 연결하기 위해서 사용하는 방식으로 매트릭을 맞추는 방법을 말한다.
1. OSPF의 매트릭을 RIP 매트릭으로 재분배 (rip으로 가서 ospf하는 말을 알아듣도록 통역)
```
router(conifg) # router rip
router(conifg) # redistribute ospf 1 metric 1
```

2. RIP의 매트릭을 OSPF 매트릭으로 재분배(ospf한테 가서 rip이 하는 말을 알아듣도록 통역)
```
router(conifg) # router ospf 1
router(conifg) # redistribute rip subnets
```
