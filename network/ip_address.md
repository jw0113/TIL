## __IP Address__
___
### __IPv4__
+ 총 32bit로 구성 (8bit.8bit.8bit.8bit)
+ 8bit를 10진수로 변환하여 표현
+ Logical Address(논리적 주소)
+ 8bit의 한 세트에 최저 값은 0, 최고 값은 255이다.
<br><br>

### __IP Address__
+ TCP/IP 프로토콜 장비를 구분해주기 위한 주소
+ TCP/IP를 사용하는 네트워크에 연결되 장비들은 고유의 IP를 가진다.
+ Network ID가 같으면 같은 네트워크 안에 있는 것이므로 통신이 가능하다.
+ IP Address = Network ID + Host ID (ex. 교실이름 + 학생번호)
+ Host ID로 장비 구분
+ 하나의 네트워크란, Router를 거치지 않고 통신이 가능한 영역
<br><br>

### __Subnet mask__
+ IP에서 Network ID와 Host ID를 구분하는 역할
+ 논리 AND연산을 이용해 구분한다.
+ Subnet Mask는 이진수로 표현할 때 1이 연속으로 들어온다. ex) 1010은 잘못된 형태
+ Network field에 1, Host field에 0을 할당한 형태
+ 논리 AND연산 후 나온 결과 값의 Host영역에 모두 0을 할당하면 Network ID이다.
+ 논리 AND연산 후 나온 결과 값의 Host영역에 모두 1을 할당하면 Broadcast 주소이다.
+ Network ID와 Broadcast주소는 IP로 사용할 수 없다.
<br><br>

### __Prefix(Subnet Mask의 다른 표현 방법)__
+ Subnet Mask의 1이 들어간 bit 숫자
+ 255.0.0.0 = /8
+ 255.255.0.0 = /16
+ 255.255.255.0 = 24
+ 255.255.255.128 = /25

<br><br>

### __IP Address Class__
+ IP 주소 범위에 따라 Subnet Mask를 Default 값으로 정한 것을 말한다.
1. Class A (0 ~ 127)
   - [형태] 0NNNNNNN.Host.Host.Host -> 앞쪽 8bit의 범위가 0 ~ 127인 경우
   - Default Subnet Mask : 255.0.0.0 (/8)
   - Network : 128  /  Host : 16,777,214
   - Host 개수가 가장 많다.
2. Class B (128 ~ 191)
   - [형태] 10NNNNNN.Network.Host.Host -> 앞쪽 8bit의 범위가 128 ~ 191인 경우
   - Default Subnet Mask : 255.255.0.0 (/16)
   - Network : 16.384  /  Host : 65,534
3. Class C (192 ~ 223)
   - [형태] 110NNNNN.Network.Network.Host -> 앞쪽 8bit의 범위가 192 ~ 223인 경우
   - Default Subnet Mask : 255.255.255.0 (/24)
4. Class D (224 ~ 239)
   - [형태] 1110MMMM.Multicast Group.Multicast Group.Multicast Group -> 앞쪽 8bit의 범위가 224 ~ 239인 경우
   - Multicast용으로 사용한다.
5. Class E (240 ~ 255)
   - 실험용으로 예약된 주소이다.
   - 255.255.255.255 -> Broadcast IP Address로 예약된다.

<br><br>

### __Classful : Subnet Mask 기준으로 네트워크를 표현한 것__

### __Subneting : IP를 효율적으로 낭비없이 분배하기 위해 Broadcast Domain의 크기를 작게 나누는 방법 (CLassful Network를 여러개의 Network로 나누는 것)__
+ subneting할 땐 Network의 Host개수가 동일하게 진행되어야 한다.
+ Subnet의 첫번째 (Host부분이 모두 0)와 마지막 (Host부분이 모두 1) IP주소는 사용하지 않는다.
+ 나눠진 Network는 이제 다른 Network이기 때문에 Router를 통해야만 통신이 가능하다. (서로 영향 주지 않는다.)