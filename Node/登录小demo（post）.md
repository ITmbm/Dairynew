#### 前端html
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

        let uv = user.value.trim();
        let pv = pw.value.trim();
        if(uv && pv){
            fetch('/login',{
                body:new URLSearchParams({
                    user:uv,
                    pw:pv
                }).toString(),
                method:'post',
                headers:{
                    'Content-Type':'application/x-www-form-urlencoded'
                }
            })
            .then(e=>e.json())
            .then(data=>{
                if(data.code === 1){
                    tanFn(data.msg);
                    // console.log(data.msg);
                }
                if(data.code === 0){
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
                console.log(data);
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
#### 后台js代码
```
const http = require('http');
const fs = require('fs');
const qs = require('querystring');

/*
    /login?user=xxx&pw=12345

    code:
        1   参数错误
        2   不存在用户
        3   密码错误
        0   成功

    let temp = '';  //user=xxx&pw=12345
    //每接收一次数据就会调用一次 data
    req.on('data', function(data){    
        temp += data;
    });

    req.on('end',()=>{
        console.log(temp);
        res.write();
        res.end();
    })
 

*/
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
let msg = {code:0,msg:'成功'};
http.createServer((req,res)=>{
    let url = req.url;
    console.log(url);
    //接口
    if(url == '/login'){
        let temp = '';
        req.on('data',(data)=>{
            temp += data;
        });
        req.on('end',()=>{
            let obj = qs.parse(temp);
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
            res.write(JSON.stringify(msg));
            res.end();
        });
           
    }else{
        //静态文件
        if(url==='/')url = '/1_login.html'; // www/1_login.html
        
        try {
            let data = fs.readFileSync('./www'+url);
            res.write(data);
        } catch (error) {
            res.write('404');
        }
        res.end();
    }
    console.log(req.url);

}).listen(80);





```