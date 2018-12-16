let xhr = new XMLHttpRequest()
#### 属性
```
xhr.response 响应的主体内容

xhr.responseText 响应主体的内容是字符串（JSON或者XML格式字符串都可以）

xhr.responseXML 响应的内容是XML文档

xhr.readyState === 2   响应头信息已经回来了
console.log(xhr.getResponseHeader('date'))字符串形式格林尼治时间，
new Date （传入）变成北京时间

xhr.readyState === 4
console.log(xhr.responseText)
响应主体内容

xhr.status http状态码

xhr.statusText 状态码的描述

xhr.timeout 设置请求超时的时间
（xhr.timeout = 1000
  xhr.ontimeout = ()=>{
      alert('请求超时，请稍后重试')
  }）
  
xhr.withCredentials 是否允许跨域（false不允许）
  
  
```
#### 方法
```
xhr.abort() 强制中断AJAX请求
（
      xhr.abort();
  xhr.onabort = ()=>{
      console.log('当前请求已经被强制中断')
  }
  ）
  
xhr.getAllResponseHeaders()获取所有的响应头信息

xhr.getResponseHeader([key])获取key对应的响应头信息，例如：xhr.getResponseHeader('date')获取响应头中的服务器时间

xhr.open() 打开URL请求

xhr.overrideMimeType() 重写Mime类型

xhr.send() 发送AJAX请求

xhr.setRequestHeader() 设置请求头
xhr.setRequestHeader('name','xiaomin')注意：不可出现中文，且必须设置在open之后














```