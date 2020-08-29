[영상 강의](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-%EC%9E%85%EB%AC%B8-%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8/lecture/49573?tab=note)

<br>
<br>

### 1. Thymeleaf 템플릿 엔진

<br>

    html 파일을 띄울 수 있게 도와주는 템플릿 엔진이다. 
    템플릿 엔진이란 html과 같은 문서를 출력하는 소프트웨어를 말한다.

### 2. Controller 

<br>

    웹 어플리케이션에서 첫 번째 진입점이다.  
    
![1](https://github.com/butcher313/TIL/blob/master/image/1.JPG)


    컨트롤러는 @Controller라는 annotation을 써준다.
    * annotation : 메타-테이터(Meta-Data) : 데이터를 위한 데이터를 의미하며, 풀어 이야기하면 한 데이터에 대한 설명을 의미하는 데이     터. (자신의 정보를 담고 있는 데이터)
    
    hello라는 페이지에 대한 GET 요청이 들어오면 스프링이 만든 model을 통해 "hello!!"라는 데이터를 넘겨주며
    컨트롤러는 최종적으로 "hello"라는 페이지를 반환한다. 
    
    그러면 view resolver는 페이지를 받아서 템플릿 엔진을 통해 hello.html에 "hello!!"를 반영하고 
    이를 랜더링한다.
    
<br>

![2](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810829/2.JPG)

<br>

![3](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810829/3.JPG)

<br>

    위의 이미지에서 ${data} 이부분이 hello!!로 바뀌게 된다. 
    
<br>
<br>

### 3. 빌드하고 실행하기

<br>

![4](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810829/4.JPG)

    cmd를 통해 프로젝트 폴더로 이동, gradlew.bat build 명령어로 빌드한다. 
    
<br>

![5](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810829/5.JPG)

    그러면 .jar 파일이 생성되는데 이를 자바로 실행시킨다. 
    
<br>

![6](https://github.com/butcher313/TIL/blob/master/image/%EC%8A%A4%ED%94%84%EB%A7%810829/6.JPG)

    위와같이 html 페이지가 잘 뜨는것을 볼 수 있다.

    
