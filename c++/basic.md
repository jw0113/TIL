## C++ 개요
---

### __C++__
+ C 개념에 Class라는 개념을 더해서 사용하는 것 의미
+ 객체 지향 특징
+ 캡슐화, 자료은닉, 상속성과 재사용성, 다형성의 특징을 지니고 있다.

<br>

### __출력문__
```c++
// 문자 출력 -> 결과: C
std::cout << 'C';

// 문자와 문자열 연달아 출력 -> 결과: C++
std::cout << 'C' << "++";

// 개행
std::cout << "Programming" << std::endl;
```

<br>

### __변수__
```c++
// 변수 선언
int num;
num = 5;
std::cout << "num의 값 : " << num << std::endl;

num = 15;
std::cout << "num의 값 : " << num << std::endl;

// <결과>
// num의 값 : 5
// num의 값 : 15
```

<br>

### __초기화__
1. 복사 초기화 (copy initialization)
2. 직접 초기화 (direct initialization)
3. 유니폼 초기화 (uniform initialization)

```c++
// 초기화
int num = 20;
std::cout << "복사 초기화한 num의 값 : " << num << std::endl;

int num1(20);
std::cout << "직접 초기화한 num의 값 : " << num1 << std::endl;

int num2(num1);
std::cout << "초기화 값이 변수인 num2의 값 : " << num2 << std::endl;

int num3{20};
std::cout << "유니폼 초기화한 num3의 값 : " << num3 << std::endl;

// <결과>
// 복사 초기화한 num의 값 : 20
// 직접 초기화한 num의 값 : 20
// 초기화 값이 변수인 num2의 값 : 20
// 유니폼 초기화한 num3의 값 : 20
```
