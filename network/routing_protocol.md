## __Routing Protocol__
---
### __Routing : Packet을 수신했을 때 목적지까지의 최적의 경로를 찾아서 전송하는 역할__

<br>

### __Routing Table__
+ 최적의 경로들이 저장되어 있는 테이블
+ 최적의 경로만 올리고 나머지 경로는 데이터베이스에 저장한다.
+ 테이블에 목적지 정보가 없는 packet은 전부 폐기(Drop)한다. (Switch 경우 Flooding 진행 - Frame을 모두 보내서 학습)
+ 'show ip route' 명령어를 통해 확인

<br>

### __Routing Protocol__
+ 목적지 네트워크로 가는 경로를 알아내기 위해 사용하는 프로토콜
+ 이를 이용해 직접 연결되지 않은 네트워크 정보를 Routing Table에 추가
+ 라우팅 프로토콜을 설정하지 않으면 직접 연결된 주소만 table에 나타난다.

<br>

### __Routing Protocol 종류__
1. Static Routing Protocol (정적 라우팅 프로토콜)
   - 관리자가 직접 경로를 입력하는 방법
   - 경로를 한번 설정하면 무조건 그 경로로만 전송한다.
    1. 장점
        - 경로 계산을 하지 않기 때문에 속도가 빠르며 메모리를 적게 사용하여 성능이 좋다.
        - routing table을 교환하지 않아 대역폭 절약
        - 자신의 정보를 외부로 보내지 않아 보안에 좋다.
    2. 단점
        - 관리자가 일일이 입력해야 하기 때문에 불편함
        - 경로에 문제가 발생해도 계속해서 그 경로로 packet을 전송한다.


2. Dynamic Routing Protocol (동적 라우팅 프로토콜)
   - 설정된 Routing Protocol 알고리즘이 최적 경로를 찾아서 Routing Table에 올린다.
   - 같은 Protocol이 설정된 Router가 서로의 네트워크 정보를 교환하면서 업데이트한다.
   - Protocol들은 각자 최적 경로를 선택하는 기준이 다르기 때문에 다른 Protocol은 서로 정보 교환을 하지 않는다.
   - 1순위의 경로가 문제가 발생할 경우 다음 순위의 경로가 올라온다.
   1. 종류
        - Distance Vector 라우팅 프로토콜 : 순수 물리적(거리, 방향)으로 최적 경로를 결정 ex) RIP, IGRP
        - Link-State 라우팅 프로토콜 : 링크의 상태(인터페이스 상태)로 최적 경로 결정 ex) OSPF, IS-IS
        - Hybrid 라우팅 프로토콜 ex) EIGRP
   2. 장점
        - 관리자가 일일이 설정하지 않아도 되므로 편리하다.
        - 선택된 경로에 문제가 발생시 스스로 새로운 경로를 찾아서 전송한다.
   3. 단점 
        - 라우터가 계산해야 하므로 cpu, memory 사용량이 크다.
        - 라우터의 부담이 크다.

<br>

### __정적 라우팅 프로토콜 이용해 수동으로 경로 설정하는 방법__
```markdown
ip route 목적지주소 Subnet Mask next-Hop address or exit interface
```
+ 목적지 주소 :  학습시킬 주소 (Network ID로 입력)
+ next-Hop address : 목적지로 가는 길의 연결된 상대방 Router의 인터페이스 주소
+ exit interface : 자신의 인터페이스 중 목적지로 가기위해 데이터가 나가야하는 인터페이스 출구 주소
