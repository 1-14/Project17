# Project17

# Project17

## Firefox记住密码插件的实现

Firefox将密码储存在"logins.json"文件中，如下图

![image](https://github.com/1-14/Project17/blob/main/1.png)

从图中可以看到，存储了"hostname","formSubmitURL","encryptedUsername","encryptedPassword"等信息，发现密码是在加密后被存储。

### 具体实现

1.记住密码

火狐浏览器自动记住密码是在监控到post登录请求后，从上往下，找到最后一个type=‘password’的input框，然后询问你是否记住该密码；如果选择记住该密码，火狐浏览器会将密码加密后写入"logins.json"文件中。

2.填充密码

火狐浏览器自动填充是从上而下，寻找第一个为type=‘password’的input框，并把值填充进去，不管这个input是否是隐藏（display:none）的。

### 存在的问题

当页面在输入密码时存在前端加密情况时，火狐浏览器在监控到post登录请求时获取到的密码为前端加密过的密码，会导致将已经加密过的密码当做密码存储下来。

## 谷歌浏览器记住密码插件的实现

谷歌浏览器将密码存储在"Login Data"文件中，如下图

![image](https://github.com/1-14/Project17/blob/main/2.png)

从图中可以看到一些和登录有关的信息，由于未使用过谷歌浏览器，所以没有存储的密码，图中乱码应为解码方式错误导致的。

## 具体实现

谷歌浏览器插件在记住密码时，会先检查表单当中是否包含以下元素
 1. 为了遵循同源策略，需要域名：lichenglong.pw
 2. 需要一个<form>标签
 3. 需要id或name为username的用户名<input>表单项
 4. 需要id或name为password的密码<input>表单项

所以，当我们发送登录请求后，浏览器检测到上述元素，会首先询问我们是否要记住密码，如果需要，将会把密码、url等关键信息加密后存储在本地的"Login Data"文件中。
