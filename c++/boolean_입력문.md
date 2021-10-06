## __Boolean & �Է¹�
---

### __Boolean__
+ True or False ���� ������ �� �ִ� �ڷ���
+ ���� : bool ������;
```c++
// boolean
bool b = true;

// True of False ���� ���ڿ��� ��� ����
std::cout << std::boolalpha;

std::cout << "b�� �� : " << b << std::endl;

// ���ڿ��� ����ϴ� ����� ���� ����
std::cout << std::noboolalpha;

std::cout << "b�� �� : " << b << std::endl;

// <���>
// b�� �� : true
// b�� �� : 1
```

<br>

### __�Է¹�__
```c++
// �Է¹�
// 1. ���� �Է� �ޱ�
int num;
std::cout << "�Է� : ";
std::cin >> num;
std::cout << "��� : " << std::endl;

// <���>
// �Է� : 30
// ��� : 30

// 2. ���� �Է� �ޱ� -> ������ ���ڷ� �Էµ��� �ʴ´�.
char ch;
std::cout << "�Է� : ";
std::cin >> ch;
std::cout << "��� : " << ch << std::endl;

// <���>
// �Է� : A
// ��� : A

// 3. �Ǽ� �Է� �ޱ�
double fnum;
std::cout << "�Է� : ";
std::cin >> fnum;
std::cout << "��� : " << fnum << std::endl;

// <���>
// �Է� : 12.12
// ��� : 12.12

// 4. �Ǽ� �Է� �ޱ� - �Ҽ��� �����ϱ� (serf�� precision ���ÿ� ����ؾ� �Ѵ�.)
double fnum1;
std::cout << "�Է� : ";
std::cin >> fnum1;
std::cout.serf(std::ios::fixed);
std::cout.precision(4);
// precision() �Լ��� �ܵ����� ����� ��� ������ ���ڸ�ŭ �������� �ڸ����� ����Ͽ� ��µȴ�.
std::cout << "��� : " << fnum1 << std::endl;
// serf() ����� ���� ���ؼ� -> std::cout.unserf(std::ios::fixed) ����Ѵ�.

// <���>
// �Է� : 12.1212
// ��� : 12.1212

// 5. ���� ���� ������ �Է� �ޱ�
int num1, num2;
std::cout << "�� �� �Է� : ";
std::cin >> num1 >> num2;
std::cout << "��� : " << num1 << ' ' << num2 << std::endl;

// <���>
// �� �� �Է� : 10 20
// ��� : 10 20

// 6. ���� ���� �Է� �ޱ�
char str;
std::cout << "�Է� : ";
std::cin.get(str);
std::cout << "��� : " << str << std::endl;

// <���>
// �Է� : 
// ��� : 
```