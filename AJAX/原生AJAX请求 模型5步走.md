#### AJAX模型
```
电话模式


1.先有一个电话     创建ajax对象 new XMLHttpRequest 适用于高版本
2.输入号码(拨号)   填写请求地址  xhr.open('请求的方式','url地址+具体的参数',是否异步（默认为true）)
3.发送             send()
4.等待             xhr.onload
5.成功接收         在xhr.onload中接收到数据 xhr.responseText
```
#### 验证用户名（get请求方式）
```
   btn.onclick = function(){
        let xhr = new XMLHttpRequest; //1.创建ajax对象
        xhr.open('get','/get?user='+txt.value,true); //是否异步  2.填写请求地址
        xhr.send();//3发送
        xhr.onload = function(){ //4.等待服务器响应
            // console.log(xhr.responseText); //5.接收的信息
            let data = JSON.parse(xhr.responseText);
            
            if(data.code == 0){
                txt.className = 'error';
            }else if(data.code == 1){
                txt.className = 'ok';
            }
        }
   };
```
##### 或者直接简化（get请求方式）
```
btn.onclick = function(){
 fetch('/get?ren='+txt.value)
        .then((e)=>e.json())
        .then(data=>{
            console.log(data);
        });
        }
```
#### post请求方式
```  
btn.onclick = function(){
        let xhr = new XMLHttpRequest;
        xhr.open('post','/post',true);
        //设置头信息
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
        xhr.send('user='+txt.value);
        xhr.onload = function(){
            console.log(JSON.parse(xhr.responseText));
        }

        // fetch('/post',{
        //     method: 'post',
        //     headers: {
        //         'Content-Type': 'application/json'
        //     },
        //     body:JSON.stringify({'user':txt.value})
        // }).then(e=>e.json())
        // .then(e=>{
        //     console.log(e);
        // });
    }

```
