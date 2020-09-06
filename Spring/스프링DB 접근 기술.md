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

