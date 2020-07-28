
Flask & mongoDB 이메일 인증
==========================  

- 파이썬으로 이메일 전송하는 코드  

``` python
  import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from random import randint

me = "butcher3130@gmail.com"
my_password = "foavkq250"
you = "2pac_777@naver.com"

## 여기서부터 코드를 작성하세요.
msg = MIMEMultipart('alternative')
msg['Subject'] = "이메일 인증"
msg['From'] = me
msg['To'] = you

#html = '<html><body><p>Hi, I have the following alerts for you!' + str(randint(1000, 9999)) +'</p></body></html>'
temp = str(randint(1000, 9999))
html = '인증 번호 : ' + temp
part2 = MIMEText(html, 'html')

msg.attach(part2)
## 여기에서 코드 작성이 끝납니다. 

# Gmail 관련 필요한 정보를 획득합니다.
s = smtplib.SMTP_SSL('smtp.gmail.com')
# Gmail에 로그인합니다. 
s.login(me, my_password)
# 메일을 전송합니다.
s.sendmail(me, you, msg.as_string())
# 프로그램을 종료합니다.
s.quit()
  ```  
<br><br/>

# 1. 회원가입 페이지   
<br><br/>

![screenshot1](/image/0728-1.JPG)  

<br><br/>

# 2. 이메일 인증 버튼 누르기
<br><br/>

![screenshot1](/image/0728-2.JPG)  

<br><br/>
#3. 이메일 인증 코드 전송
<br><br/>

![screenshot1](/image/0728-3.JPG)  

<br/>
이메일 인증 버튼을 누르면 입력한 이메일 주소로 인증번호가 전송된다. 
<br><br/>

#4. 인증번호 입력
<br><br/>

![screenshot1](/image/0728-4.JPG)  

<br><br/>
#5. 회원가입 완료
<br><br/>

![screenshot1](/image/0728-5.JPG)  

<br><br/>
#6. 로그인
<br><br/>

![screenshot1](/image/0728-6.JPG)  

<br><br/>
#7. 메인 화면
<br><br/>

![screenshot1](/image/0728-7.JPG)  

<br><br/>


