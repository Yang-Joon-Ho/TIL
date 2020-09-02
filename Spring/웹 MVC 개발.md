[영상](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49589?tab=note)
-----------------------------------------------------------------

<br>
<br>

### 1. 회원 웹 기능 - 홈 화면 추가

<br>

![1](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810902/1.JPG)

    HomeController라는 새로운 컨트롤러를 생성하고, localhost:8080에 접속하면 home.html이 뜨도록 한다. 
    
<br>

### 2. 회원 등록
<br>

![2](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810902/3.JPG)

![3](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810902/2.JPG)

![4](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810902/4.JPG)


    html파일을 보면 form action = "/members/new" method="POST" 문구가 있다. 이를 통해 MemberController의 
    create 메소드가 실행이 되고, 스프링이 html의 name="name"을 보고 input에 입력된 값을 MemberForm의 name에 넣어주어
    MemberForm 객체가 생성이 된다. 그럼 member 객체에서 이를 받아 setName()을 하고 최종적으로 
    memberService.join()의 매개변수로 넘겨주게 된다.
    
    만약에 MemberForm의 setName(String name)에서 name을 name이 아닌 다른 단어로 바꾸면 html input에서 입력한 name 값이 서버에 전달이 안된다. 
    
    
    정리하자면 html 페이지를 띄우고 form을 submit 할 때, input에 입력한 name 값을 서버에 전달, PostMapping에 의해 MemberConrtoller의 
    create(MemberForm form) 메소드 실행, 스프링이 MemberForm 객체를 생성하면서 name을 setName() 매개변수로 넣어줌. 
    그리고 Member 객체를 생성하고, 이를 memberService.join에 넘긴다. 
    이게 회원 가입 등록 루틴이다.  
