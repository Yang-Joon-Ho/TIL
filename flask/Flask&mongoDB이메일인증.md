
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
# 3. 이메일 인증 코드 전송
<br><br/>

![screenshot1](/image/0728-3.JPG)  

<br/>

  > 이메일 인증 버튼을 누르면 입력한 이메일 주소로 인증번호가 전송된다. 

<br><br/>

# 4. 인증번호 입력
<br><br/>

![screenshot1](/image/0728-4.JPG)  

<br><br/>
# 5. 회원가입 완료
<br><br/>

![screenshot1](/image/0728-5.JPG)  

<br><br/>
# 6. 로그인
<br><br/>

![screenshot1](/image/0728-6.JPG) 

<br><br/>

  > 회원가입을 완료하면 로그인 페이지로 넘어오게 된다. 

# 7. 메인 화면
<br><br/>

![screenshot1](/image/0728-7.JPG)  

<br><br/>

- 회원 가입 js 코드
``` js
// 간단한 회원가입 함수입니다.
// 아이디, 비밀번호, 닉네임을 받아 DB에 저장합니다.
function email_auth() {
    $.ajax({
        type: "POST",
        url: "/api/email_auth",
        data: { id_give: $('#userid').val(), nickname_give: $('#usernick').val(),
        email_give: $('#useremail').val() },
        success: function (response) {
            if (response['result'] == 'success') {

                let number = response['number']

                alert('이메일로 인증번호 전송 완료')
                    let temp_html = `<div class="form-group">
                                <label for="userpw">인증번호</label>
                                <input type="text" class="form-control" id="auth_num" placeholder="인증 번호">
                            </div>`
                    
                    let button = `<button id = "${number}" class="btn btn-primary" onclick="number_auth(this.id)">인증</button>`
                    $('#email_auth_button').remove();
                    
                    $('#user').append(temp_html);
                    $('#user').append(button);
            } else {
                alert(response['msg'])
            }
        }
    })
}

function number_auth(number) {
    if($('#auth_num').val() == number){
        let button = `<button class="btn btn-primary" onclick="register()">회원가입</button>`
        alert('인증 완료')
        $('#user').append(button)
    }
    else {
        alert('인증 번호가 다릅니다.')
    }
}

function register() {
    $.ajax({
        type: "POST",
        url: "/api/register",
        data: {
            id_give: $('#userid').val(), pw_give: $('#userpw').val(),
            nickname_give: $('#usernick').val(), email_give: $('#useremail').val()
        },
        success: function (response) {
            if (response['result'] == 'success') {
                alert('회원가입이 완료되었습니다.')
                window.location.href = 'login.html'
            } else {
                alert(response['msg'])
            }
        }
    })
}
```

- 회원 가입 서버 코드

``` py
# [회원가입 API]
# id, pw, nickname을 받아서, mongoDB에 저장합니다.
# 저장하기 전에, pw를 sha256 방법(=단방향 암호화. 풀어볼 수 없음)으로 암호화해서 저장합니다.

#이메일 인증
@app.route('/api/email_auth', methods=['POST'])
def api_auth():

    me = "butcher3130@gmail.com"
    my_password = "foavkq250"
    
    you = request.form['email_give']
    id_receive = request.form['id_give']
    nickname_receive = request.form['nickname_give']

    ######## 동일한 이메일 주소가 db에 있는지 검색
    if len(list(db.user.find({'email' : you}))) != 0 :
        return ({'result' : 'fail', 'msg' : '해당 email로 가입한 기록이 있습니다.'})
    elif len(list(db.user.find({'id' : id_receive}))) != 0 :
        return ({'result' : 'fail', 'msg' : '해당 id가 이미 존재합니다.'})
    elif len(list(db.user.find({'nick' : nickname_receive}))) != 0 :
        return ({'result' : 'fail', 'msg' : '해당 닉네임이 이미 존재합니다.'})
    ########

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

    
    return jsonify({'result': 'success', 'number' : temp})

@app.route('/api/register', methods=['POST'])
def api_register():
    id_receive = request.form['id_give']
    pw_receive = request.form['pw_give']
    nickname_receive = request.form['nickname_give']
    email_receive = request.form['email_give']

    ######기존에 있는 id 혹은 닉네임인지 확인
    if len(list(db.user.find({'id' : id_receive}))) != 0 :
        return ({'result' : 'fail', 'msg' : '해당 id가 이미 존재합니다.'})
    elif len(list(db.user.find({'nick' : nickname_receive}))) != 0 :
        return ({'result' : 'fail', 'msg' : '해당 닉네임이 이미 존재합니다.'})
    ######

    pw_hash = hashlib.sha256(pw_receive.encode('utf-8')).hexdigest()

    db.user.insert_one({'id':id_receive,'pw':pw_hash,'nick':nickname_receive, 'email':email_receive})
    
    return jsonify({'result': 'success'})

# [로그인 API]
# id, pw를 받아서 맞춰보고, 토큰을 만들어 발급합니다.
@app.route('/api/login', methods=['POST'])
def api_login():

   id_receive = request.form['id_give']
   pw_receive = request.form['pw_give']

   # 회원가입 때와 같은 방법으로 pw를 암호화합니다.
   pw_hash = hashlib.sha256(pw_receive.encode('utf-8')).hexdigest()

   # id, 암호화된pw을 가지고 해당 유저를 찾습니다.
   result = db.user.find_one({'id':id_receive,'pw':pw_hash})

   # 찾으면 JWT 토큰을 만들어 발급합니다.
   if result is not None:
      # JWT 토큰에는, payload와 시크릿키가 필요합니다.
      # 시크릿키가 있어야 토큰을 디코딩(=풀기) 해서 payload 값을 볼 수 있습니다.
      # 아래에선 id와 exp를 담았습니다. 즉, JWT 토큰을 풀면 유저ID 값을 알 수 있습니다.
      # exp에는 만료시간을 넣어줍니다. 만료시간이 지나면, 시크릿키로 토큰을 풀 때 만료되었다고 에러가 납니다.
      payload = {
         'id': id_receive,
         #'exp': datetime.datetime.utcnow() + datetime.timedelta(seconds=30)
      }
      token = jwt.encode(payload, SECRET_KEY, algorithm='HS256').decode('utf-8')

      # token을 줍니다.
      return jsonify({'result': 'success','token':token})
   # 찾지 못하면
   else:
      return jsonify({'result': 'fail', 'msg':'아이디/비밀번호가 일치하지 않습니다.'})

# [유저 정보 확인 API]
# 로그인된 유저만 call 할 수 있는 API입니다.
# 유효한 토큰을 줘야 올바른 결과를 얻어갈 수 있습니다.
# (그렇지 않으면 남의 장바구니라든가, 정보를 누구나 볼 수 있겠죠?)
@app.route('/api/nick', methods=['GET'])
def api_valid():
   # 토큰을 주고 받을 때는, 주로 header에 저장해서 넘겨주는 경우가 많습니다.
   # header로 넘겨주는 경우, 아래와 같이 받을 수 있습니다.
   token_receive = request.headers['token_give']

   # try / catch 문?
   # try 아래를 실행했다가, 에러가 있으면 except 구분으로 가란 얘기입니다.

   try:
      # token을 시크릿키로 디코딩합니다.
      # 보실 수 있도록 payload를 print 해두었습니다. 우리가 로그인 시 넣은 그 payload와 같은 것이 나옵니다.
      payload = jwt.decode(token_receive, SECRET_KEY, algorithms=['HS256'])

      # payload 안에 id가 들어있습니다. 이 id로 유저정보를 찾습니다.
      # 여기에선 그 예로 닉네임을 보내주겠습니다.
      userinfo = db.user.find_one({'id':payload['id']},{'_id':0})
      return jsonify({'result': 'success','id':userinfo['id']})
   except jwt.ExpiredSignatureError:
      # 위를 실행했는데 만료시간이 지났으면 에러가 납니다.
      return jsonify({'result': 'fail', 'msg':'로그인 시간이 만료되었습니다.'})

```

