---
layout: post
title : 1. JDBC, SQL mapper, ORM, Jpa에 대해 알아보자!!.
subheading: 개인정리용 글입니다. 틀린부분있을수도 있음.
author: Donghui Lee
categories: SpringBoot 기본

banner:
    image: /assets/images/banners/computer.jpg
    subheading_style: "color: gold"
tag: [SpringBoot, jpa, 스프링부트 스타트]

---
> 구멍가게 코딩단의 스타트 스프링부트책을 바탕으로 정리함.  

  

처음 스프링부트에 입문하여 책을 이리저리 보다보니 `JDBC`, `SQL mapper`, `ORM`, `JPA`, `Hibernate`등등 여러 용어가 나와서 상당히 했갈려해서 다음과 같이 정리하였다.

## 1. 개념정리
일단 먼저 개념을 알아보면 

JDBC(Java Database Connectivity)
- 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 **API**이다  


ORM(Object-relational mapping)
- 객체와 관계형 데이터베이스의 데이터를 자동으로 매핑(연결)해주는 것 추상화된 **개념**일뿐  


SQL Mapper
- Object와 SQL의 필드을 매핑하여 데이터를 객체화하는 **기술**  


JPA(Java Persistence API)
- Java 관련 기술 스펙의 하나이며 데이터를 관리,유지하는 기법을 하나의 스펙으로 정리한 **인터페이스 표준**  


Hibernate
- JPA의 **구현체**  

Spring data Api
- spring framework에서 JPA를 편리하게 사용할 수 있도록 지원하는 프로젝트  


> Api : API는 Application Programming Interface(애플리케이션 프로그램 인터페이스)의 줄임말  


## 2. SQL Mapper
**<정의>**
- Object와 SQL의 필드을 매핑하여 데이터를 객체화하는 기술.  
- 객체와 테이블간의 관계를 매핑하는 것이 아니라, SQL문을 직접 작성하고 쿼리 수행결과를 어떠한 객체에 매핑하여 줄 지 바인딩하는 방법. 즉 SQL **의존적인** 방법이다.  

ex) JdbcTemplate, Mybatis
 
o MyBatis
: SQL을 xml파일로 분리하여 관리하고, SQL결과와 객체 인스턴스의 매핑을 도와주는 역할을 수행.  
동적쿼리를 지원하여 다이나믹하게 변경되는 쿼리 작성가능.  
 

--> SQL을 개발자가 직접 작성하는 문제.  
--> DBMS에 종속적인 문제.  
--> 비슷한 쿼리를 반복적으로 작성해야하는 문제  
--> 객체와 관계형 테이블 구조간 패러다임 불일치 발생.    


## 3. ORM
**<정의>**
- Object와 DB테이블을 매핑하여 데이터를 객체화하는 기술.  
- CRUD 관련 메소드를 사용하면 자동으로 SQL이 만들어져 개발자가 반복적인 SQL을 직접 작성하지 않아도 되고, DBMS에 종속적이지 않다.
- 또한 복잡한 쿼리의 경우 JPQL을 사용하거나 SQL Mapper를 혼용하여 사용할 수 있다.  
- Java ORM 기술에 대한 인터페이스 표준을 **JPA**라고 하고, 이를 구현한 가장 대표적인 기술이 **Hibernate**이다.  

ex) Hibernate, EclipseLink, DataNucleus  

--> DBMS에 의존하지 않음으로써 도메인과 비즈니스 로직 설계에 더 집중할 수 있는 장점  
--> 요구사항 변화에 빠른 대처 가능한 장점  
--> 복잡한 통계성 쿼리보다는 실시간 처리용 쿼리에 적합  

### 3-1. Spring Data Jpa(Repository)
spring framework에서 JPA를 편리하게 사용할 수 있도록 지원하는 프로젝트
- CRUD 처리를 위한 공통 인터페이스 제공
- repository 개발 시 인터페이스만 작성하면 실행 시점에 스프링 데이터 JPA가 구현 객체를 동적으로 생성해서 주입
- 데이터 접근 계층을 개발할 때 구현 클래스 없이 인터페이스만 작성해도 개발을 완료할 수 있도록 지원
- 공통 메소드는 스프링 데이터 JPA가 제공하는 org.springframework.date.jpa.repository.JpaRepository 인터페이스에
  count, delete, deleteAll, deleteAll, deleteById, existsById, findById, save ..  

< 참고그림 >
 ![image](/assets/images/banners/springboot_Start/springdatajpa.png)


## 4. 결론

정리하자면  
1. 데이터의 영속성(persistence)을 위해 Java에서는 JDBC를 지원해 줌.  
2. 이 JDBC는 DB에 접근해서 SQL을 수행하고 결과값을 다시 dataType으로 매핑시켜주는 작업을 함.  
=> 상당히 귀찮음.
3. 근데 매번하기 귀찮으니까 나온 개념이 SQL mapper와 ORM이 있다.  
=> 개발자가 직접 JDBC프로그래밍을 하지않는다!! 둘다 Persistence Framework의 종류이다.  
4. SQL mapper와 ORM은 둘다 기술(개념?)일뿐이고 구현체는 대표적으로 SQL mapper에는 Mybatis, JDBC Template가 있고 ORM의 구현체로는 Hibernate, EclipseLink등등이있다.
5. JPA는 어디에 들어가는가? JPA는 java에서 ORM 개념을 구현하기위한 스펙이고 ORM이 일종의 비젼에 불과했다면, JPA는 이를 구현하기위한 상세한 통과기준  
=> ORM(기초 개념) -> JPA(심화 개념) -> Hibernate(구현체!!)

> 영속성 : 프로그램이 종료되어도 사라지지 않고 어떤 곳에 저장되는 것
 



## 5. 그림정리
* 이미지 새탭으로 열어서 보세요.  

![image](/assets/images/banners/springboot_Start/JpaV2.png)  

## 6. 출처

* 참고  
https://deveun.tistory.com/entry/SQL-Mapper%EC%99%80-ORM-%EC%B0%A8%EC%9D%B4

* spring data jpa 참고 블로그  
https://data-make.tistory.com/621  

* jpa vs springdata Jpa
https://suhwan.dev/2019/02/24/jpa-vs-hibernate-vs-spring-data-jpa/

