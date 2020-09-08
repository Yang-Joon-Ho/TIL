[영상](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49601?tab=curriculum)
-----------------------------------------------------------------------------

<br>
<br>

### 1. AOP 적용 

<br>

![1](https://github.com/butcher313/TIL/blob/master/image/0908/AOP/1.JPG)


<br>

#### 1) AOP를 스프링 빈에 등록하는 방법

![2](https://github.com/butcher313/TIL/blob/master/image/0908/AOP/2.JPG)

<br>

    위와 같이 @Component를 사용하여 Component 스캔으로 스프링 빈에 등록해도 되고, 
    
![3](https://github.com/butcher313/TIL/blob/master/image/0908/AOP/3.JPG)

<br>

    아니면 이렇게 SpringConfig에다가 @Bean으로 등록해주어도 된다. 그런데 @Bean으로 등록하는 경우 
    추가작업을 해줘야 하는데 여기서 안가르쳐주므로 그냥 넘어가자.
    
<br>
<br>

#### 2) AOP 적용한 상태에서 서버 돌리고 console 확인해 보기

![4](https://github.com/butcher313/TIL/blob/master/image/0908/AOP/4.JPG)

    서버를 돌리면 가장 처음에 memberService가 실행된다.
    
<br>

![6](https://github.com/butcher313/TIL/blob/master/image/0908/AOP/6.JPG)
![5](https://github.com/butcher313/TIL/blob/master/image/0908/AOP/5.JPG)

    회원 등록 페이지에서 회원 등록을 하고 조회를 한 이후의 log 창이다. 
    
    AOP는 매서드 호출이 될 때 조건에 맞으면 딱 걸리게 하는? 것으로써 
    여기서는 모든 매서드를 대상으로 시간을 측정했지만 원하는 매서드만 볼 수 있도록 할 수도 있다.
    
<br>

#### 3) AOP 적용 후 의존관계

![7](https://github.com/butcher313/TIL/blob/master/image/0908/AOP/7.JPG)

    AOP 적용 후에는 프록시라는 기술을 사용하여 가짜 Service 클래스를 만들어서 Controller와 연결 시킨 후,
    joinPoint.proceed()가 호출될 때, 진짜 Service를 실행시킨다. 
    
    아마 컨트롤러가 동작하면서 Service를 호출하려 할때, Service는 AOP로 등록이 되어있고, joinPoint.proceed()를 통해 
    실행이 되어야 하므로 AOP를 통해 동작 시키기 위해 가짜 Service를 실행하는것 같다. 
   
<br>
    
#### 4) AOP 적용 후 전체 그림

![8](https://github.com/butcher313/TIL/blob/master/image/0908/AOP/8.JPG)
    
