## __Boolean & 입력문
---

### __Boolean__
+ True or False 값을 저장할 수 있는 자료형
+ 형식 : bool 변수명;
```c++
// boolean
bool b = true;

// True of False 값을 문자열로 출력 가능
std::cout << std::boolalpha;

std::cout << "b의 값 : " << b << std::endl;

// 문자열로 출력하는 기능을 끄는 역할
std::cout << std::noboolalpha;

std::cout << "b의 값 : " << b << std::endl;

// <결과>
// b의 값 : true
// b의 값 : 1
```

<br>

### __입력문__
```c++
// 입력문
// 1. 정수 입력 받기
int num;
std::cout << "입력 : ";
std::cin >> num;
std::cout << "출력 : " << std::endl;

// <결과>
// 입력 : 30
// 출력 : 30

// 2. 문자 입력 받기 -> 공백은 문자로 입력되지 않는다.
char ch;
std::cout << "입력 : ";
std::cin >> ch;
std::cout << "출력 : " << ch << std::endl;

// <결과>
// 입력 : A
// 출력 : A

// 3. 실수 입력 받기
double fnum;
std::cout << "입력 : ";
std::cin >> fnum;
std::cout << "출력 : " << fnum << std::endl;

// <결과>
// 입력 : 12.12
// 출력 : 12.12

// 4. 실수 입력 받기 - 소수점 설정하기 (serf와 precision 동시에 사용해야 한다.)
double fnum1;
std::cout << "입력 : ";
std::cin >> fnum1;
std::cout.serf(std::ios::fixed);
std::cout.precision(4);
// precision() 함수를 단독으로 사용할 경우 설정한 숫자만큼 정수부터 자리수를 계산하여 출력된다.
std::cout << "출력 : " << fnum1 << std::endl;
// serf() 기능을 끄기 위해선 -> std::cout.unserf(std::ios::fixed) 사용한다.

// <결과>
// 입력 : 12.1212
// 출력 : 12.1212

// 5. 여러 개의 데이터 입력 받기
int num1, num2;
std::cout << "두 수 입력 : ";
std::cin >> num1 >> num2;
std::cout << "출력 : " << num1 << ' ' << num2 << std::endl;

// <결과>
// 두 수 입력 : 10 20
// 출력 : 10 20

// 6. 공백 문자 입력 받기
char str;
std::cout << "입력 : ";
std::cin.get(str);
std::cout << "출력 : " << str << std::endl;

// <결과>
// 입력 : 
// 출력 : 
```