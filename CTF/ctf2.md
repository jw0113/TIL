### __문제__
```markdown
Jensen 사건을 맡게 된 Jack과 그의 팀은 Jensen의 회사와 가정에 네트워크 탭과 무선 캡처 장비를 설치했다. 
모니터링을 하는 동안 Jack과 그의 팀은 흥미로운 용의자인 Betty를 발견했다. 
이 사람은 Jensen 부인이 남편과 바람을 피고 있다고 걱정하는 여자일 수도 있다. 
Jack은 포렌식 전문가인 당신에게 캡쳐 정보를 자세히 보여준다. 그리고 회의가 진행된다. 
Round 1 패킷을 사용해서 사건에 대해 자세히 알아보고 다음의 질문에 답하시오.

회의가 예정된 요일은 언제인가?
```
---

### __파일__ : round1.pcap
<br>
round1.pcap을 Wireshark를 통해 패킷 분석한다. <br>
패킷들 중 IRC프로토콜로 통신한 기록을 발견했다. <br>
<br>

### __IRC프로토콜로 통신한 패킷 분석__
```
PRIVMSG #S3cr3tSp0t :Hi Greg :)
:D34thM3rch4nt!~blah2@7FF07A37.29E7D414.B9027CEB.IP PRIVMSG #S3cr3tSp0t :Hi Betty
:D34thM3rch4nt!~blah2@7FF07A37.29E7D414.B9027CEB.IP PRIVMSG #S3cr3tSp0t :what day do you want to meet up?
PING :hades.de.eu.SwiftIRC.net
PONG :hades.de.eu.SwiftIRC.net
PING :hades.de.eu.SwiftIRC.net
PONG :hades.de.eu.SwiftIRC.net
PING :hades.de.eu.SwiftIRC.net
PONG :hades.de.eu.SwiftIRC.net
PRIVMSG #S3cr3tSp0t :&#x48;&#x6F;&#x77;&#x20;&#x64;&#x6F;&#x65;&#x73;&#x20;&#x57;&#x65;&#x64;&#x6E;&#x65;&#x73;&#x64;&#x61;&#x79;&#x20;&#x73;&#x6F;&#x75;&#x6E;&#x64;&#x3F;
:D34thM3rch4nt!~blah2@7FF07A37.29E7D414.B9027CEB.IP PRIVMSG #S3cr3tSp0t :&#x47;&#x72;&#x65;&#x61;&#x74;&#x20;&#x3A;&#x29;&#x20;&#x77;&#x68;&#x61;&#x74;&#x20;&#x74;&#x69;&#x6D;&#x65;&#x3F;
PRIVMSG #S3cr3tSp0t :&#x61;&#x68;&#x20;&#x32;&#x70;&#x6D;
:D34thM3rch4nt!~blah2@7FF07A37.29E7D414.B9027CEB.IP PRIVMSG #S3cr3tSp0t :&#x4F;&#x6B;&#x2C;&#x20;&#x49;&#x20;&#x63;&#x61;&#x6E;&#x27;&#x74;&#x20;&#x77;&#x61;&#x69;&#x74;&#x21;
```
Greg과 Betty의 대화 내용을 확인할 수 있다.<br>
여기서 언제 만날 것인지에 대한 응답은 HTML 인코딩되어 있음을 알 수 있다.
<br>

### __HTML 디코딩__
[디코딩 전]
```
PRIVMSG #S3cr3tSp0t :&#x48;&#x6F;&#x77;&#x20;&#x64;&#x6F;&#x65;&#x73;&#x20;&#x57;&#x65;&#x64;&#x6E;&#x65;&#x73;&#x64;&#x61;&#x79;&#x20;&#x73;&#x6F;&#x75;&#x6E;&#x64;&#x3F;
:D34thM3rch4nt!~blah2@7FF07A37.29E7D414.B9027CEB.IP PRIVMSG #S3cr3tSp0t :&#x47;&#x72;&#x65;&#x61;&#x74;&#x20;&#x3A;&#x29;&#x20;&#x77;&#x68;&#x61;&#x74;&#x20;&#x74;&#x69;&#x6D;&#x65;&#x3F;
PRIVMSG #S3cr3tSp0t :&#x61;&#x68;&#x20;&#x32;&#x70;&#x6D;
:D34thM3rch4nt!~blah2@7FF07A37.29E7D414.B9027CEB.IP PRIVMSG #S3cr3tSp0t :&#x4F;&#x6B;&#x2C;&#x20;&#x49;&#x20;&#x63;&#x61;&#x6E;&#x27;&#x74;&#x20;&#x77;&#x61;&#x69;&#x74;&#x21;
```
[디코딩 후]
```
PRIVMSG #S3cr3tSp0t :How does Wednesday sound?
:D34thM3rch4nt!~blah2@7FF07A37.29E7D414.B9027CEB.IP PRIVMSG #S3cr3tSp0t :Great :) what time?
PRIVMSG #S3cr3tSp0t :ah 2pm
:D34thM3rch4nt!~blah2@7FF07A37.29E7D414.B9027CEB.IP PRIVMSG #S3cr3tSp0t :Ok, I can't wait!
```

디코딩 결과 : Wednesday 2시에 만나기로 했다.

## __정답 : Wednesday__
