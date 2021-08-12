## __RIP__
---
### __RIP__
1. 특징
   + Distance Vector Routing Protocol
   + IP 네트워크를 이용해 주위에 인접한 라우팅 정보를 교환하여 최적의 경로를 찾는다.
   + AD 값 : 120 -> 목적지가 같은 라우팅 프로토콜이 여러개일 때 AD값이 작은 순으로 선택된다.
   + Routing 정보 전송을 위해 UDP 포트 520번을 사용한다.
   + Metric을 Hop-count로 사용한다. (목적지까지 가는데 거치는 장비의 수)
   + 가장 적은 Hop-count를 최적 경로로 결정한다.
   + 30초마다 정보를 교환한다.

2. 장점
   + Static Routing Protocol보다 구성하기 편하고 네트워크 변화에 있어서 편하게 수정할 수 있다.
   + 작은 규모의 네트워크에 적합
   + 표준 Protocol이기 때문에 다른 회사의 Router에서 사용할 수 있다.
  
3. 단점
   + Hop-count로 경로를 결정하므로 수가 많아도 가장 빠른 길일 경우도 있을 수 있지만 RIP은 이를 무시한다.
   + 복잡한 네트워크에서는 비효율적인 Routing 경로가 설정될 수 있다.
   + 최대 Hop-count은 15이기 때문에 이 이상을 넘어가면 도달 불가능한 네트워크로 간주한다. 따라서 대규모의 네트워크에서는 비효율적이다.
   + 무조건 30초마다 정보를 교환해야 하므로 특별한 변화가 없을 경우에도 정보를 교환하여 비효율적이다.

<br>

### __RIP Version__
1. Version 1
   - Subnet Mask 정보가 없는 Classful 라우팅 프로토콜
   - 정보 전송 시 Broadcast 주소를 사용한다.
   - 브로드캐스트로 전달하므로 RIP이 설정되지 않은 장비들에게는 불필요한 부하가 걸린다.
2. Version 2
   - Subnet Mask 정보가 있는 Classless 라우팅 프로토콜
   - 정보 전송 시 Multicast 사용
   - Version 2를 가장 많이 사용한다.

<br>

### __Convergence Time__
+ Convergence : 네트워크 변화가 생길 경우 상태에 대해 정확하고 일관된 정보를 유지하는 것
+ 네트워크 변화 발생 시 변화된 정보를 인식하고 수정하는 시간
+ Protocol마다 Convergence Time이 서로 다르다.
+ 시간이 짧을수록 좋다.

<br>

### __RIP의 Convergence TIme__
+ RIP의 Convergence Time은 30초로 느리다.
+ 따라서, Routing Loop 문제가 발생할 수 있다.

<br>

### __RIP의 Routing Loop 문제 해결 방법__
1. Split Horizon : 정보 얻은 쪽의 인터페이스에서 다시 그 방향으로 정보를 보내지 않는 방식. 같은 정보가 나가는 것을 방지함.
2. Route Poisoning : 연결이 끊긴 부분은 Hop-count를 최대로 늘려 더이상 이 경로를 이용할 수 없도록 만드는 방식
3. Hold Down Time : 받은 정보를 다른 라우터에게 보내지 않고 일정 시간 기다려서 잘못된 정보인지 파악하는 방식
4. Triggered Update : 변화가 발생했을 시 Convergence Time이 안되었더라도 바로 알려주는 방식

<br>

### __RIP 연결 방법__
```markdown
Router(config) # router rip
Router(config) # version 2
Router(config) # no auto-summary
Router(config) # network 네트워크 아이디
```
+ 자신이 가지고 있는 모든 네트워크 아이디를 입력한다.
+ Privilege Mode에서 'show ip route'를 입력해 설정을 확인한다.
+ 모든 설정이 완료되면 스스로 학습한다.