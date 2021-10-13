## __std::string__
---
<br>

### __std::string__
+ '#include <string>' 헤더파일 포함해주어야 한다.
```c++
// std::string 입출력
std::string str;
std::cout << "입력 : ";
std::cin >> str;
std::cout << "출력 : " << str << std::endl;

// <결과>
// 입력 : hello
// 출력 : hello

// 초기화
std::string str = "Hello";
std::cout << "str 출력 : " << str << std::endl;

std::string str1(5, 'a');
std::cout << "str1 출력 : " << str1 << std::endl;

std::string str2 = "Hello";
std::cout << "str2 출력 : " << str2[0] << str2[1] << str2[2] << str2[3] << str2[4] << std::endl;

// <결과>
// str 출력 : Hello
// str1 출력 : aaaaa
// str2 출력 : Hello
```

<br>

### __std::getline()__
+ 문자열을 입력받을 때 공백을 포함하여 전체 라인을 입력 받은 함수
+ 첫 번째 매개변수는 입력방식, 두 번째 매개변수는 저장할 변수 작성
```c++
// std::getline()

std::string str;
std::cout << "입력 : ";
std::getline(std::cin, str);
std::cout << "출력 : " << str << std::endl;

// <결과>
// 입력 : Hello world
// 출력 : Hello world
```