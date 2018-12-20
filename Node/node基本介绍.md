#### 基本介绍
```
 Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境,
 node 文件名 可以运行某个js文件
 这个js文件可以写后台语言
 Node.js 的包管理器 npm，是全球最大的开源库生态系统。
 
特点：

单线程
事件驱动 某个条件完后执行
无阻塞I/O 执行任务时，不阻塞通道

事件驱动编程（Evnet-driven programming）是一种编程风格，由事件来决定程序的执行流程，事件由事件处理器（event handler）或事件回调（event callback）来处理，事件回调是当某个特定事件发生时被调用的函数，比如数据库返回了查询结果或者用户单击了一个按钮。

非阻塞I/O模型 在操作系统中，程序运行的空间分为内核空间和用户空间。我们常常提起的异步I/O，其实质是用户空间中的程序不用依赖内核空间中的I/O操作实际完成，即可进行后续任务。

qs.parse可以把url的查询信息字段转成对象

file system模块用来操作文件。增删改查文件
```
#### 快餐店举例
```
在快餐店点餐吃饭的场景。

我们同样是要发起请求，等待服务器端响应；但是与银行例子不同的是，这次我们点完餐后拿到了一个号码，拿到号码，我们往往会在位置上等待，而在我们后面的请求会继续得到处理，同样是拿了一个号码然后到一旁等待，接待员能一直进行处理。

等到饭菜做号了，会喊号码，我们拿到了自己的饭菜，进行后续的处理（吃饭）。这个喊号码的动作在NodeJS中叫做回调（Callback），能在事件（烧菜，I/O）处理完成后继续执行后面的逻辑（吃饭），这体现了NodeJS的显著特点，异步机制、事件驱动整个过程没有阻塞新用户的连接（点餐），也不需要维护已经点餐的用户与厨师的连接。

```
#### 应用
```
NodeJS适合运用在高并发、I/O密集、少量业务逻辑的场景。

 Web聊天室(IM)
 Web爬虫
 Web论坛
 大量Ajax请求的应用
```
#### 基本操作
- 可以在node中打印
```
新建一个js文件
打开node，输入node 文件名
console(8+8)//node中输出16
```
- 一个js文件中导出，另一个中请求导入
```
导出
module.exports = {
    a:10
};
导入
let obj = require('文件路径,文件名不用加js');
```
- 读取响应url地址
```
引入http，就是到默认文件夹下找一个叫 http.js 的文件

 ***http是没有加路径的，因为它是自带的，如果要用一个自己定义的js文件
那么基本上要写路径。

=============================
语法
let http = require('http');
http.createServer((request,response)=>{
    // console.log(request);
    let name = request.url.split('=')[1];
     // console.log( request.url.split('=')[0])//  /?name
    switch(name){
        case 'xyz':
            response.write('{code:0,msg:chy}');
        break;
        case 'hongdan':
            response.write('{code:0,msg:cmy}');
        break;
        default:
            response.write('{code:1,msg:cyy}');
        break;
    }
    response.end();
}).listen(80);

```
```
处理汉语
let http = require('http');
http.createServer((request,response)=>{
    // console.log(request)//拿到客户端输入的信息，例如url后面的hongdan
let name = request.url.split('=')[1];
response.writeHead(200, {'Content-Type': 'text/html; charset=utf-8'});
switch(decodeURI(name)){
    case 'tianqi':
    response.write('晴朗');
    break;
    case 'meimei':
    response.write('longnv');
    break;
    default:
    response.write('meimei');
    break;
}

    response.end()
}).listen(80)
```
```
let http = require('http');
let qs = require('querystring');
//创建一个80的端口服务
http.createServer((req,res)=>{

    let url = req.url.split('?');
    let obj = qs.parse(url[1]);//
    把查询信息字段转成对象

    res.write('hehe');
    res.end();

}).listen(80); //listen(80)监听80端口
```
##### 操作文件 增删改查
- 读取文件
```
/* 
    fs.readFile(path,callback);

        callback(error,data)

        当有数据返回data就是读出来的文件。
*/

```
```
const fs = require('fs');

fs.readFile('./www/1.txt',(error,data)=>{
    if(error){
        console.log('404');
    }else{
        console.log(data.toString());
    }
});
//或者
try {
    let data = fs.readFileSync('./www/1.txt');
    console.log(data.toString());
} catch (error) {
    
}
console.log(11111);
```
======================
```
let http = require('http');
http.createServer((request,response)=>{
    // console.log(request)//拿到客户端输入的信息，例如url后面的hongdan
let name = request.url.split('=')[1];
response.writeHead(200, {'Content-Type': 'text/html; charset=utf-8'});
switch(decodeURI(name)){
    case 'tianqi':
    response.write('晴朗');
    break;
    case 'meimei':
    response.write('longnv');
    break;
    default:
    response.write('meimei');
    break;
}

    response.end()
}).listen(80)
```
- 写文件和删文件
```
let fs = require('fs');

fs.writeFile('./www/2.txt','dsnadkjsjdksa',(error)=>{
    if(error){
        console.log('失败');
    }else{
        console.log('成功');
    }
})

fs.unlinkSync('./www/2.txt'); //删除指定的文件
```
打开node，
npm init
输入ex


























