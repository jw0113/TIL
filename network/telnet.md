## __Telnet__
---

### __Telnet__
+ 라우팅 프로토콜 종류 중 하나인 원격 접속 프로토콜
+ 라우터에서 설정을 구성할 수 있다.
+ 장점 - 물리적으로 떨어져있는 라우터를 설정하고자 할 때 실제로 자신이 움직일 수 없는 경우 원격 접속을 통해서 설정할 수 있다.
+ 단점 - 보안에 취약하다.

<br><br>

### __Telnet 설정 방법__
```
// Telnet은 라우터 패스워드를 지정하지 않으면 관리자 모드로 들어갈 수 없으므로 password 설정 먼저 진행한다.
router(config) # enable password 비밀번호

// 원격 접속을 위한 가상 터미널을 열어서 접속한다.
// 아래의 명령어는 가상 터미널인 vty의 0번부터 4번까지 연다는 의미이다.
router(config) # line vty 0 4

// Telnet의 기본 형태는 login해야 접속할 수 있으므로 로그인에 해당하는 paswword 설정한다.
router(config) # password 비밀번호
router(config) # login
```
+ vty는 0번 ~ 15번까지 총 16개가 존재한다.
+ 'no login' 명령어를 입력하면 로그인하지 않는 형태로 변환할 수 있다.


<br><br>

### __Telnet 접속 방법__
1. PC에서 Command Prompt로 접속한다.
2. 'telnet PC와 연결 가능한 라우터의 인터페이스ID'를 입력해 접속한다.
ex) telnet 192.168.10.254