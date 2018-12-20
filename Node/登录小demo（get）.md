#### 前端html（get请求数据）
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
<style>
#tan{
    width:100px;
    height:30px;
    background: skyblue;
    color: #fff;
    padding: 5px;
    text-align: center;
    line-height: 30px;
    position: absolute;
    top:-40px;
    left:50%;
    margin-left:-60px;
    transition: top 500ms;
}

</style>
</head>
<body>
    用户名:  <input type="text" id="user">
    密码:<input type="password" id="pw">
    <button id="btn">登录</button>
    <div id="tan">不存在用户</div>
<script>
    /*
        1   参数错误
        2   不存在用户
        3   密码错误
        0   成功
    */
    btn.onclick = function(){
       //获取拿到用户名和密码
        let uv = user.value.trim();
        let pv = pw.value.trim();
        //都填写了的情况下
        if(uv && pv){
        //fetch请求，把这一堆发送给后台，里面有用户名和密码
            fetch('/login?user='+uv+'&pw='+pv) 
            //把后台res.write()里面的字符串（json）数据格式转成对象，并返回一个promise对象，里面的resolve后面的值就是要传给下面then的第一个函数的实参
            .then(e=>e.json())
            .then(data=>{
                if(data.code === 1){
                    tanFn(data.msg);
                    // console.log(data.msg);
                }
                if(data.code === 0){
                //有callback函数
                    tanFn(data.msg,()=>{
                        window.location.href = 'http://www.zhufengpeixun.cn';
                    });
                }
                if(data.code === 2){
                    tanFn(data.msg);
                }
                if(data.code === 3){
                    tanFn(data.msg);
                }
                <!--console.log(data);-->
            });
        }
    }

    function tanFn(txt,cb){
        tan.innerHTML = txt;
        tan.style.top = '30%';
        setTimeout(()=>{
            tan.style.top = '-40px';
            setTimeout(function(){
                cb && cb();
            },500);
        },2000);
    }
</script>
</body>
</html>
```
#### 后台代码（node中运行），相当于开服务器
```
const http = require('http');
//操作文件命令
const fs = require('fs');
//把查询信息转成对象命令
const qs = require('querystring');

/*
    /login?user=xxx&pw=12345

    code:
        1   参数错误
        2   不存在用户
        3   密码错误
        0   成功

*/
//diy数据库
let sql = [
    {
        name:'cyy',
        pw:12345
    },
    {
        name:'cmy',
        pw:4321
    },
    {
        name:'luoben',
        pw:1234
    }
];
//准备返回给前端的响应信息
let msg = {code:0,msg:'成功'};
http.createServer((req,res)=>{
    //req和res都是对象，实例化对象
    //拿到前端的url值
    let url = req.url;
    //包含？说明是点击了登录按钮
    if(url.includes('?')){
    //拿到后面的查询信息
        let arr = url.split('?');
        //把查询信息转成对象
        let obj = qs.parse(arr[1]);
        //登录
        if(arr[0]==='/login'){
            // console.log(/^\w{2,8}$/.test(obj.user))
            if(obj.user && obj.pw && /^\w{2,8}$/.test(obj.user)){
                res.writeHead(200,{'Content-Type':'text/html; charset=utf-8'});
                /*
                    到底有没有这个人
                */
               let u = sql.find(e=>obj.user == e.name);
               if(u){ //有这个人才判断密码是否正确
                    if(u.pw == obj.pw){ //密码对不对
                        msg.code = 0;
                        msg.msg = '成功';
                    }else{
                        msg.code = 3;
                        msg.msg = '用户或密码错误~!';
                    }
               }else{
                    msg.code = 2;
                    msg.msg = '用户不存在';
               }

            }else{
                msg.code = 1;
                msg.msg = '参数错误';
                res.writeHead(400,{'Content-Type':'text/html; charset=utf-8'});
            }
            // res.write(JSON.stringify(msg));
            res.write('郑文会')
            res.end();
        }
    }else{
        //静态文件
        if(url==='/')url = '/1_login.html'; // www/1_login.html
        
        try {
            let data = fs.readFileSync('./www'+url);
            res.write(data);
        } catch (error) {
            res.write('404');
        }
        
        // fs.readFile('./www'+url,(error,data)=>{
        //     if(error){
        //         console.log('404');
        //     }else{
        //         res.write(data)
        //     }
        // });
        res.end();
    }
    console.log(req.url);

}).listen(80);





```
