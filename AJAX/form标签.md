#### 用法
```
<form> 标签用于为用户输入创建 HTML 表单。

form 元素是块级元素

表单用于向服务器传输数据。

name:前后端协商好的字段

<form action="form_action.asp" method="get">
  <p>First name: <input type="text" name="fname" /></p>
  <p>Last name: <input type="text" name="lname" /></p>
  <input type="submit" value="Submit" />
</form>
```
#### 属性
```
action	URL
规定当提交表单时向何处发送表单数据。

method	get/post/delete/put
规定用于发送 form-data 的 HTTP 方法
```
