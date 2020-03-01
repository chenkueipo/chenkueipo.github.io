## Session: 儲存用戶訊息

### 設置密鑰
透過 os.urandom 函數隨機產生 12 bytes 的字串做為密鑰
```python
from flask import Flask
import os

app = Flask(__name__)
app.config.update(dict(
    SECRET_KEY = os.urandom(12)
))
```

<br/>

### 模擬用戶登入重新導向
本例示範用戶從 /login 頁面拜訪，儲存紀錄至 session 後轉址至 /hello 頁面。
```python
from flask import session, redirect, url_for

@app.route('/login')
def login():
    session['logged_in'] = True
    return redirect(url_for('hello'))
    
@app.route('/greet')
def hello():
    return "Hello Flask!"
```
<br/>

### 登出用戶
本例示範用戶拜訪 /logout 頁面後清空 session 的登入紀錄，並轉址至 /goodbye 頁面。
```python
from flask import session, redirect, url_for

@app.route('/logout')
def logout():
    if 'logged_in' in session:
        session.pop('logged_in')
    return redirect(url_for('goodbye'))
    
@app.route('/goodbye')
def hello():
    return "Goodbye Flask!"
```

<br/><br/><br/>

[回到Blog首頁](../index.md)

<br/>