## __ACL__
---

### __ACL (Access Control List)__
+ 특정 트래픽의 접근을 허용할지 차단할지 결정하는 리스트 (filtering)
+ Application Layer부분까지 관리하기 때문에 Network Layer이라고 단정할 수 없다.
+ Firewall 등의 전문적인 보안 장비를 사용한다.

<br><br>

### __ACL 종류__
1. Standard Access List
   + 출발지 주소만 보고 Permit or Deny 여부를 결정하는 ACL이다. 
   + 출발지와 ACL에 정의된 출발지주소가 일치하면 ACL의 내용을 수행한다.
   + Permit - packet을 정해진 경로로 전송 / Deny - packet의 흐름을 차단
   + List-Number : 1 ~ 99번까지 사용
  
2. Extended Access List
   + 출발지 주소외에 목적지 주소, Protocol, Port 번호 등의 좀 더 자세한 정보를 참조해서 filtering 여부를 결정한다.
   + ip, tcp, udp, icmp 등의 상세 프로토콜을 선택해서 결정
   + 라우팅 프로토콜도 차단 가능
   + List-Number : 100 ~ 199번까지 사용
  
3. Named ACL
   + 숫자로 구분하는 것이 아닌 이름을 이용하여 filtering 설정을 진행
   + 중간에 수정이 가능하다는 특징을 가지고 있다.

<br><br>

### __ACL 설정 방법__
1. Standard Access List
```
Router(config)# access-list 번호 permit or deny 출발지주소 wildcard mask
// 만일 출발지주소를 deny로 설정한 경우 - 나머지 주소들은 허용함을 설정해준다.
Router(config)# access-list 번호 permit any
Router(config)# interface 인터페이스명
Router(config)# ip access-group 번호 in or out
```
   + in : 라우터의 인터페이스로 packet이 들어오는 경우를 막음
   + out : 라우터에서 해당 인터페이스로 나가는 경우를 막음
<br><br>

2. Extended Access List
```
Router(config)# access-list 번호 permit or deny 프로토콜 출발지주소 wildcard mask 목적지주소 wildcard mask 포트
// 만일 permit으로 설정한 경우 - 나머지 주소들은 차단함을 설정해준다.
Router(config)# access-list 번호 deny 프로토콜 any any
Router(config)# interface 인터페이스명
Router(config)# ip access-group 번호 in or out
```
<br>

3. Named ACL
```
Router(config)# ip access-list standard or extended Access-List이름
// 차단하는 경우
Router(config)# deny 주소 wildcard mask
// 허용하는 경우
Router(config)# permit 주소 wildcard mask
Router(config)# interface 인터페이스명
Router(config)# ip access-group access-list이름 in or out
```
<br><br>

### __ACL 규칙__
1. ACL은 순서대로 수행되기 때문에 좁은 범위를 먼저 진행해야 한다.
2. ACL 마지막은 'deny any'가 기본값으로 생략되어 있다. 따라서 permit any가 없을 경우 ACL 조건에 없는 모든 주소는 deny형태로 되어 있다.
3. standard와 exteded는 중간에 수정 및 삭제가 불가능하지만 named는 수정이 가능하다.