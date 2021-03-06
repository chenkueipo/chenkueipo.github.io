## Route

### 1. 綁定多個 URL
本例將 say_hello() 同時註冊 '/hi' 及 '/hello' 兩個 URL
```python
@app.route('/hi')
@app.route('/hello')
def say_hello():
	return "Hello Flask!"
```

### 2. 綁定包含變數的 URL
本例 URL 所帶的變數名稱為 name，且預設為 name='Guest'。
```python
@app.route('/greet')
@app.route('/greet/<name>')
def say_hello(name='Guest'):
	return "Hello, {}!".format(name)
```

### 3. 使用 redirect() + url_for() 管理專案內的 URL 
透過重新導向的方式，讓專案內僅需出現一次相同的 URL 字串。  
本例中 url_for('say_hello', name='Guest') = "/greet/Guest"
```python
from flask import Flask, redirect, url_for
app = Flask(__name__)

@app.route('/greet/<name>')
def say_hello(name):
    return "Hello, {}!".format(name)

@app.route('/')
def index():
	return redirect(url_for('say_hello', name='Guest'))
```

<br/><br/><br/>

[[回到Flask文章列表]](index.md)  
