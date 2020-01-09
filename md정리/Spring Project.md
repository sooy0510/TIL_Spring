# Spring Project

## 1. 프로젝트 생성

### 1. 스프링 기반의 웹 프로젝트 생성

- [File] -> [New] -> [Spring Legacy Project]

  - **Spring MVC Project** 선택

    <br>
    
    ![1576158640954](images/1576158640954.png)

<br>

<br>

- 패키지 지정

  - 패키지 경로에 최소 세 개 이상의 패키지가 지정되어야 프로젝트 생성 가능

    <br>


<br>

<br>

##  2. 스프링 IoC 시작하기

### 2.1 스프링 설정 파일 생성

<br>

### 2.2 스프링 컨테이너의 종류

-  BeanFactory
- ApplicationContext(BeanFactory를 상속)

<br>

<br>

#### 2.2.1 BeanFactory

> 스프링 설정 파일에 등록된 <bean> 객체를 생성하고 관리하는 가장 기본적인 컨테이너 기능만 제공

<br>

- 컨테이너가 구동될 때 `<bean>` 객체를 생성하는 것이 아니라, 클라이언트의 요청(**Lookup**)에 의해서만 `<bean>`객체가 생성되는 **지연 로딩(Lazy Loading) 방식**을 사용

  *=> 따라서 일반적인 스프링 프로젝트에서 BeanFactory를 사용할 일은 전혀 없다!!!*

<br>

<br>

#### 2.2.2 ApplicationContext

> BeanFactory가 제공하는 <bean> 객체 관리 기능 외에도 **트랜잭션 관리나 메시지 기반의 다국어 처리** 등 다양한 기능을 지원한다

<br>

- **컨테이너가 구동되는 시점**에 `<bean>` 등록된 클래스들을 객체 생성하는 즉시 로딩(pre-loading) 방식으로 동작
- 웹 애플리케이션 개발도 지원하므로 대부분 스프링 프로젝트는 ApplicationContext 유형의 컨테이너를 이용

- 대표 ApplicationContext구현 클래스
  - GenericXmlApplicationContext
  - **XmlWebApplicationContext** : 웹 기반의 스프링 애플리케이션을 개발할 때 사용하는 컨테이너