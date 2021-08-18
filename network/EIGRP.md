## __EIGRP__
---
### __EIGRP__
+ RIP + OSPF
+ DUAL (Diffusing Update Algorithm) 알고리즘을 이용하여 최적 경로(Successor)와 후속 경로(Feasible Successor)을 선출
+ Convergence Time이 빠르다.
+ 최적 경로에 문제가 발생할 경우 후속 경로를 최적경로로 올린다.
+ AD값 : 내부 - 90 / 외부 - 170
+ AS (Autonomous System)단위로 구성
+ Classless Routing Protocol

1. 장점
   - Fast convergence time : DUAL 알고리즘을 통해 후속 경로까지 구하므로 수정이 빠르다.
   - Unequal Cost 부하 분산 지원 - 하나의 일을 여러 장비가 나눠서 진행
   - OSPF에 비해 설정 간단
2. 단점
   - Cisco전용이므로 Cisco Router에서만 작동
   - 대규모 네트워크에서는 관리가 힘들다.
   - SIA현상 발생 가능 - 후속 경로가 없을 경우 주변 Router에게 물어보는데 응답 기다리는 시간이 길어지는 현상을 말한다.

<br><br>

### __EIGRP Packet__
1. Hello Packet
   - Neighbor을 구성하고 유지하는 packet
   - 기본적으로 Hello interval의 3배 해당하는 시간안에 상대방의 Hello Packet을 받지 못할 경우 Neighbor 해제
2. Update Packet
   - 라우팅 정보를 전송할 때 사용하는 packet
3. Query Packet
   - 라우팅 정보를 요청할 때 사용하는 packet
   - 자신의 Routing Table에 있는 경로가 다운되거나 대체 경로가 없을 시 해당 경로에 대한 정보 요청할 때 사용한다.
4. Reply Packet
   - Query Packet을 수신한 Router가 라우팅 정보를 전송할 때 사용하는 Packet (Query Packet)
   - 유니캐스트로 전송
5. Acknowledgement Packet
   - Update, Query, Reply Packet의 수신을 확인할 때 사용한다.
   - Ack, Hello Packet에 대해서는 확인하지 않는다.
   - 유니캐스트로 전송


<br><br>

### __EIGRP 동작 과정__
1. EIGRP가 라우팅 경로를 계산하는 절차<br>
   1) Hello Packet을 교환해 Neighbor 관계를 맺고 Neighbor table 생성
   2) Update Packet을 통해 라우팅 정보를 교환하고 Topology Table 생성
   3) Topology Table 정보를 조합하여 최적 경로를 계산하고 Routing Table에 저장
2. 특정 네트워크로 가는 경로가 다운되었을 경우 (= 네트워크에 변화가 생겼을 경우)<br>
   1) Query Packet으로 라우팅 정보를 요청하고 응답 상태 테이블 생성
   2) Reply Packet을 수신하여 Topology Table에 저장
   3) 수신한 정보를 조합하여 최적 경로를 계산하고 Routing talbe에 저장

<br><br>

### __EGIRP Metric__
+ ((10^7 / 가장 느린 bandwidth) + (모든 delay를 합한 값 / 10)) * 256

<br><br>

### __DUAL (Diffusing Update Algorithm)__
1. FD (Feasible Distance) : 출발지에서 목적지까지 계산한 EIGRP Metric 값 (최적 Metric)
2. AD (Advertised Distance) : 출발지 Router의 Next-hop라우터에서 목적지까지 계산한 EIGRP Metric값
3. Successor : FD값이 가장 낮은 경로 상의 Next-hop 라우터
4. Feasible Successor : 최적 경로가 동작하지 못할 때 계산없이 바로 Routing Table에 등록되는 후속 경로로 Successor를 제외한 나머지 중 AD값이 FD값보다 작은 경우가 선출

<br><br>

### __EIGRP 설정 방법__
```
router(conifg) # router eigrp as번호
router(conifg) # no auto-summary
router(conifg) # network 네트워크ID wildcard mask
```

<br>

### __B/W와 DLY 값 변경 방법__
```
router(conifg) # interface 인터페이스명
// B/W를 변경하는 경우
router(conifg) # bandwidth 범위 값
// Delay 값을 변경하는 경우
router(conifg) # delay 범위 값
```
+ 'show interface 인터페이스명'을 입력해 설정을 확인할 수 있다.
+ 값 변경 시 단위를 조심해야 한다. - dealy 2000 -> 20000이 실제로 설정됨

<br><br>

### __두 AS끼리 연결하는 방법__
```
router(conifg) # router eigrp 100
router(conifg) # no auto-summary
router(conifg) # network IP주소 wildcard mask
router(conifg) # exit
router(conifg) # router eigrp 200
router(conifg) # no auto-summary
router(conifg) # network IP주소 wildcard mask
router(conifg) # exit

//재분배
router(conifg) # router eigrp 100
router(conifg) # redistribute eigrp 200
router(conifg) # exit
router(conifg) # router eigrp 200
router(conifg) # redistribute eigrp 100
router(conifg) # exit
```
+ 각 AS에 들어가서 재분배를 진행해야 한다.

<br><br>

### __EIGRP와 OSPF를 연결하는 방법__
```
//경계 router에서 인터페이스 설정 진행
router(conifg) # interface serial 0/3/1
router(conifg) # router ospf 1 -> 이후 ospf 설정과 동일하게 진행
router(conifg) # exit
router(conifg) # interface serial 0/3/0
router(conifg) # router eigrp 100 -> 이후 eigrp 설정과 동일하게 진행

//재분배
router(conifg) # router ospf 1
router(conifg) # redistribute eigrp 100 subnets
router(conifg) # exit
router(conifg) # router eigrp 100
router(conifg) # redistribute ospf 1 metrix 대역폭 지연시간 1 1 1
```