#### 步骤
```
1、与服务器交互的文件不可放在中文文件夹下，在public文件下新建
2、在node下打开服务器 （helloworld 打开node，输入node app.js）
3、在浏览器输入localhost/XX.html打开文件(不可双击打开)

```
#### jQuery下的数据交互
总结：
```
$.ajax({
    url:必须传,请求地址   后台提供
    data:{
        人:穆宝民
        key(为前后端一起定义的字段):前端传的数据（如表单类value）
    }
    success:function(data){
    data -> 原为json，转为object，直接使用的数据
}
});
```
##### 验证注册用户名
```
     $('#btn').click(function(){
         $.ajax({
             url:'/get',
             data:{user:$('#txt').val()},
             success:function(json){
                 let data = JSON.parse(json);
                 if(data.code === 1){
                     alert('可以注册')
                 }else if(data.code === 0){
                     alert('名字重复')
                 }
             }
         })
     })
```
##### 渲染音乐的数据
数据在
http://localhost/player
```
  $('#btn').click(function(){
        $.ajax({
            url:'/player',//后台给的
            data:{
                json:'true'//后台和你一起定
            },
            dataType:'json',
            success:function(data){
                // console.log(data);
                if(data.code === 0){
                    let temp = '';
                    data.msg.forEach(d => {
                        // if(d.filename.includes('【')){
                            temp += `<li>${d.filename}</li>`   
                        // }
                    });
                    console.log(data);
                    $('#ul').html(temp);
                }
            }
        });
```