# DI (Dependency Injection)

> 스프링 프레임워크의 가장 중요한 특징은 **객체의 생성과 의존관계를 컨테이너가 자동으로 관리**한다는 점이다
>
> => *IoC의 핵심 원리!!*

<br>

스프링은 IoC를 다음 두가지 형태로 지원한다

**실제 애플리케이션 개발 과정에서는 Dependency Injection을 사용해서 개발**한다

- Dependency Lookup

  - 컨데이너가 애플리케이션 운용에 필요한 객체를 생성
  - 클라이언트가 생성한 객체를 검색(Lookup)하여 사용

  <br>

- Dependency Injection

  - 컨테이너가 직접 객체들 사이에 의존관계를 처리하는 것을 의미

  - 객체 사이의 의존관계를 **스프링 설정 파일**에 등록된 정보를 바탕으로 컨테이너가 자동으로 처리해준다
  - **따라서 의존성 설정을 바꾸고 싶을 때 프로그램 코드를 수정하지 않고 스프링 설정 파일 수정만으로 변경사항을 적용할 수 있어서 유지보수가 향상**
  - DI는 다시 **세터 인젝션**과 **생성자 인젝션**으로 나뉜다

<br>

<br>

## 1. 생성자 인젝션

- 스프링 컨테이너는 XML 설정파일(applicationContext.xml)에 등록된 클래스를 찾아서 **객체 생성시 기본적으로 매개변수가 없는 Default 생성자를 호출**한다 
- 하지만 컨테이너는 생성자 인젝션을 통해 매개변수를 가지는 다른 생성자를 호출하도록 설정할 수 있다
- 생성자 인젝션을 사용하면 생성자의 매개변수로 **의존관계에 있는 객체의 주소 정보**를 전달할 수 있다
- `<constructor-arg>` 엘리먼트 사용

<br><br>

<br>

## 2. Setter 인젝션

- Setter 메소드를 호출하여 의존성 주입을 처리하는 방식

- 대부분 개발시 Setter 인젝션 사용

- Setter 메소드 내에 `this` 키워드로 객체 연결

- Setter 메소도는 스프링 컨테이너가 자동으로 호출

  => 호출시점은 `<bean>`객체 생성 직후

  => 따라서 Setter 인젝션이 동작하려면 기본 생성자도 반드시 필요하다

<br>

<br>

### 2.1 `<property>` 엘리먼트

- name` 속성 : 호출하고자 하는 메소드 이름 => ex) 속성값이 "speaker"면 호출되는 메소드는 setSpeaker( )

  <br>

- `ref` 속성 : 생성자 인젝션과 마찬가지로 Setter 메소드를 호출하면서 다른 `<bean>` 객체를 인자로 넘길 때 사용

- `value` 속성 : `<bean>` 객체 말고, 기본형 데이터 넘길 때 사용

<br>

<br>

## 2.2 p 네임스페이스

> Setter 인젝션을 설정할 때, 'p 네임스페이스'를 이용하면 좀 더 효율적인 의존성 주입이 가능하다

<br>

- 스프링 설정 파일(applicationContext.xml) 에서 네임스페이스만 선언해주면 <bean>으로 클래스(기본 생성자) 등록할 때 참조객체나 값을 바로 할당해 주는 방식

- 네임스페이스 선언

  ```xml
  // applicationContext.xml
  
  <beans xmlns="http://www.springframework.org/schema/beans"
         ...
         xmlns:p="http://www.springframework.org/schema/p"
         ...
  </beans>
  ```

  <br>

- 기본 생성자 등록

  ``` xml
  // applicationContext.xml
  
  <bean id="tv"
        class="polymorphism.SamsungTV" p:speaker-ref="sony" p:price="270000"/>
  
  <bean id="sony" class="polymorphism.SonySpeaker"/>
  ```

<br>

<br>

## 2.3 컬렉션(Collection) 객체 설정

> 프로그램을 개발하다 보면 배열이나 List같은 컬렉션(Collection) 객체를 이용하여 데이터 집합을 사용해야 하는 경우가 있다. 이 때는 컬렉션 객체를 의존성 주입하면 되고, 스프링에서는 컬렉션 매핑과 관련된 엘리먼트를 지원한다

<br>

### 2.3.1 지원 엘리먼트 종류

- `<list>`
- `<set>`
- `<map>`
- `<props>`

<br>

<br>

### 2.3.2 