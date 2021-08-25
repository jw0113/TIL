### __문제__
```
Mrs. Jensen은 이 이상한 이메일을 더 자세히 보기로 결심한다. 그녀는 계좌 잔고를 확인하기 위해 계좌에 대한 접근 권한을 계속 유지하기로 결정한다. Round 7 패킷을 사용해서 다음 질문에 답하시오.

Victoria가 지시한 허위(악의적인) 웹페이지의 URL은 무엇입니까?
```
---

### __파일 : round7.pcap__
해당 파일을 wireshark 프로그램을 이용해 실행한다.<br>
HTTP Object를 Export한 결과 bank관련 주소가 존재함을 알 수 있다.<br>

<br>

### __bank관련 주소 : www.bankofamerica.com__
해당 주소를 입력해서 들어간 결과 올바른 주소임을 알 수 있다.<br>
해당 주소와 관련된 모든 주소를 파악한 후 의심스러운 주소를 발견하였다.

<br>

### __의심스러운 주소 : bankofamerica.tt.omtrdc.net__
해당 주소를 입력하여 들어간 결과 알 수 없는 주소로 나오는 것을 확인할 수 있다.<br>
따라서 해당 주소에 대한 packet을 TCP Stream을 통해 확인해보았다. <br>

```
mboxHost=infocenter.bankofamerica.com&mboxSession=1373056092923-406506&mboxPC=1373056092923-406506.19_30&mboxPage=1373056898233-47366&screenHeight=1024&screenWidth=1280&browserWidth=1280&browserHeight=861&browserTimeOffset=-360&colorDepth=24&mboxXDomain=enabled&mboxCount=1&mbox=bac_global_bottom&mboxId=0&mboxTime=1373035298047&mboxURL=http%3A%2F%2Finfocenter.bankofamerica.com%2Fsmallbusiness%2Fic2%2Fonline-banking%2Fview-balances-account-activity%2F&mboxReferrer=http%3A%2F%2Fwww.google.com%2Furl%3Fsa%3Dt%26rct%3Dj%26q%3Dwhy%2520is%2520my%2520bank%2520of%2520america%2520account%2520not%2520working%253F%26source%3Dweb%26cd%3D2%26ved%3D0CD4QFjAB%26url%3Dhttp%253A%252F%252Finfocenter.bankofamerica.com%252Fsmallbusiness%252Fic2%252Fonline-banking%252Fview-balances-account-activity%252F%26ei%3DdS_XUdu5Gei7igLL7YHQDw%26usg%3DAFQjCNEh7nqNYvobnOUp-5_YMQJn7YTKEQ%26bvm%3Dbv.48705608%2Cd.cGE&mboxVersion=41 HTTP/1.1
```
+ packet의 내용을 살펴보면 중간에 "why is my bank america account not working"이라는 문장이 숨어져 있는 것을 알 수 있다.
<br>
<br>

### __정답 : http://bankofamerica.tt.omtrdc.net__