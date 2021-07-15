## Spring 기초
--- 
### DI 개요
DI (Dependency Injection) : 컨테이너에서 만든 각종 객체들은 서로 의존적이므로 객체를 만들어서 외부에서 따로 주입한다.

<br>

### 의존성 주입 방법
1. 생성자를 통한 의존성 주입
```java
<constructor-arg ref="Bean ID"></constructor-arg>
```

2. Setter를 통한 의존성 주입
```java
<property name="변수명" value="값"/>
<property name="변수명" ref="객체"/>
```
<br>

### Bean의 범위
1. 싱글톤(Singleton) : 컨테이너에서 생성된 빈 객체는 기본적으로 한 개만 생성된다. 따라서 getBean()메소드 호출 시, 동일한 객체만 호출되므로 값 변경 시 영향을 받는다.
2. 프로토타입(Prototype) : getBean() 메소드를 호출할 때마다 객체가 만들어진다. scope속성을 이용하여 명시한다.

<br>

### 의존 객체 자동 주입
1. @Autowired : 객체 타입으로 검색하여 의존성을 주입하는 이노테이션
2. @Qualifier("Bean ID") : 동일 타입의 bean이 여러개일 경우 어떤 bean을 주입하는지 선택하는 추가 이노테이션 (@Autowired와 함께 쓰임)
3. @Resource : name 속성을 통해 검색하여 주입하는 이노테이션