[영상](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49594?tab=note&mm=close)
-------------------------------------------------------------------------------------

<br>
<br>

### 1. h2 데이터베이스 설치 & 세팅 

<br>

![1](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/1.JPG)

    h2 DB 생성 후, id를 자동 생성하는 테이블을 만든다.
    
<br>

#### 1) 자바와 h2 데이터베이스를 연결하기 위한 작업

![2](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/build-gradle.JPG)
    
    build.gradle 수정

![3](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/%EC%A0%91%EC%86%8D%EC%A0%95%EB%B3%B4.JPG)

    applications.properties 수정, data source가 DB 접속 정보를 담고 있는 것이다.
    
<br>

### 2. 스프링 Jdbc template 

#### 1) spring config

<br>

![4](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/%EC%8A%A4%ED%94%84%EB%A7%81config.JPG)

       DB 연결에 관한 정보를 담고 있는 dataSource를 스프링 빈에 등록하고, SpringConfig 에 의존성 주입을 해주어 dataSource 객체 생성 한 후, 
       아래에 JdbcTemplateMemberRepository()의 매개변수로 넣어준다. 
       
       그래야 Jdbc에서 dataSource를 보고, DB에 접근하여 쿼리 날리고 받아온 결과를 객체에 RowMapper을 사용하여 매핑하는 등의 작업을 할 수 있다.

<br>

#### 2)JdbcTemplateMemberRepository

<br>

![5](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/jdbcTemplate1.JPG)

    JdbcInsert 생성해서 DB에 저장할 준비 하고, 테이블 이름, 키 값 설정한 다음에 
    
    hash 자료형의 parameters라는 변수 선언 후, 해당 변수에 이름을 저장한 후, 
    
    Number key = 블라블라 에서 DB에 저장을 한다. 
    그리고 저장된 member의 키 값을 받아서 member 객체를 반환한다.
    
<br>

![6](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/jdbcTemplate2.JPG)

<br>

+ RowMapper

![7](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/jdbcTemplate3.JPG)


<br>

### 3. 테스트 

<br>

![8](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/%ED%85%8C%EC%8A%A4%ED%8A%B8.JPG)

<br>

    테스트는 앞서 만들어놓은 테스트 코드와 별반 다르지 않다.
    
    다만 클래스 위에 @Transactional이라는 annotation을 적어놓음으로써 테스트 단위끼리 서로
    충돌이 일어나는 경우를 방지하였다.
    
    그리고 memberService와 memberRepository를 @Autowired로 해주었다. 따로 생성자를 만들어서 하기도 하지만 테스트에서 굳이 그럴 필요가 없다. 
    
<br>
<br>

### 4. JPA

<br>

    jpa는 인터페이스이다. 구현은 여러 업체에서 하는데 그 중 하나가 hibernate이다. jpa는 ORM(Object Relational Mapping) 개념을 사용하는데, 
    즉, 객체와 관계형 데이터베이스를 매핑한다는 얘기이다.
    
<br>

#### 1) Spring Configuration
<br>

![9](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/2.JPG)
![10](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/3.JPG)

    Entitiy manager 의존성 주입
    
<br>

#### 2) application properties

<br>

![11](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/4.JPG)

#### 3) build.gradle

<br>

![12](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/5.JPG)

<br>

#### 4) JpaMemberRepository

<br>

![13](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/6.JPG)
![14](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/7.JPG)

#### 5) Member

<br>

![15](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/8.JPG)

    private String name; 위에 annotation은 적어놓지 않아도 되지만 설명을 위해서 적었다. 

<br>

#### 6) MemberService

<br>

![16](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810906/9.JPG)


