#### 客户端和服务器端
```
客户端：  所有可以向服务器发送请求的一端都是客户端
服务器端：  所有可以接收客户端请求，并且给其响应一些内容的都是服务器端，服务器就是一台高性能电脑
```

#### url
```
 * http：//www.baidu.com/blog/login?user=zf&password=12345#b
 http ://zhufengpeixun.cn:80/stu/index.html?name=XXX&age=25#teacher
    *
    * uri url urn
    *
    * URI 统一资源标识符 //总称
    * URN 统一资源名称 //邮箱地址
    * URL 统一资源定位符 //普通链接地址
    *
    * URI= URN+URl
    
    
    encodeURI（'汉字'）
    decodeURI（'%...'）
```
#### 传输协议
```
    用来传输客户端和服务器端交互的信息的（类似于快递员，有好多家快递公司）
    
    * http：超文本传输协议 它不仅可以传输文本 还可以传输图片音视频，文件流 其他文件 它是目前大多数网站通用的传输协议，web传输协议
    *
    * https：http ssl  更安全的超文本传输协议，在客户端和服务端 进行数据连接传输的时候会进行ssl算法加密 对传输的内容 进行ssl算法加密 保证传输的数据不被劫持  这种传输协议大多应用在跟金钱包括用户隐私 和用户交易等一系列的网站当中  使用非常广泛也正因为有了加密的过程  访问会慢一点
    *
    * ftp：文件传输协议 一般用于本地文件和服务器端文件进行资源上传下载 传输的文件比较大
```
#### 域名 Domain Name
```
一级域名（顶级域名）www.qq.com
二级域名   sports.qq.com
三级域名   kbs.sports.qq.com
.com 商用的国际域名 
.cn 供商用的中文域名 
.net 用于网络供应服务商（系统类的经常使用NET域名） 
.org 用于官方组织 
.edu 用于教育 
.gov 用于政府

```

#### 端口号
```
用来区分一台服务器上不同服务的标识（基于web服务管理创建服务的时候可以指定），不同服务之间不可使用相同的端口号
    * http默认的端口是80；
    * https默认的端口是443；
    * ftp 默认的端口是21
    * 一台服务器上的端口区间 0-65535
    * webStorm 63342 ws把自己的电脑当做服务器，在服务器上创建一个服务，端口号是63342，自己电脑的浏览器预览自己的电脑上的服务，属于本机服务请求，用localhost（127.0.0.1）本地域名即可
    * 默认端口可以不用写 不是默认端口必须要把端口号写清楚(localhost:88/jq.html)
    
    *服务器上安装一款应用都可能会作为一个服务，占用一个端口号
```
#### 请求的路径名称
```
path
pathname
例如：/stu/index.html 一般都是请求当前服务对应的项目目录中，stu文件夹中的index.html文件

```
#### 剩余的部分
```
 * 文件目录 /blog/login
    * 表示当前文件对应的blog文件下login文件的index.html 文件
    *
    * 参数  user=zf&password=12345
    * 表示参数 一般用来传输给服务器端 服务端接受到这些参数后 对参数进行拆分 进行相对应的操作
    *
```
#### 查看url的？开始后面到不含#的东西
```
问号到井号之间的信息叫查询信息（也叫参数）
window.location.search
```
#### 查看 url的哈希值
```
window.location.hash
字符串#XXX
    * 【哈希值】
    *  #b 最后这个哈希值和服务端没有太大关系  一般用于前端锚点定位 或者哈希路由跳转
    ===========================
     let num = 0;
    btn.onclick = function(){
        //页面刷新,应该放在事件中
        // window.location.reload();
        // window.location = window.location;
        num++
        window.location.hash = '#p='+num;
    }

    window.onhashchange = function(){
        alert(window.location.hash.substring(1));
    }
    =============================
    let arr = ['新闻','体育','军事','头条'];
    let btns = document.getElementsByTagName('button');
    let hashNum;//为了对应btn的颜色
    let hash = window.location.hash; //一上来先获取hash
    if(!hash){//如果没有
        window.location.hash = 'p=0'; //强行设置一波0，这个时候直接就跑到了hashchange中
    }else{
        //如果有，就获取hash值
        hashNum = window.location.hash.split('=')[1]*1;
        p.innerHTML = arr[hashNum];
    }

    arr.forEach((e,i)=>{
        let btn = document.createElement('button');
        btn.innerHTML = e;
        btn.className = hashNum!=undefined && (e==arr[hashNum]?"active":'');
        btn.onclick = function(){
            // for(let i=0;i<btns.length;i++){
            //     btns[i].className = ''; 
            // }
            // this.className = 'active';
            // p.innerHTML = e;
            window.location.hash = 'p='+i;
        }
        box.appendChild(btn)
    });

    window.onhashchange = function(){
        for(let i=0;i<btns.length;i++){
            btns[i].className = ''; 
        }
        let i = window.location.hash.split('=')[1]*1;
        btns[i].className = 'active';
        p.innerHTML = arr[i];
    }
```
#### 输入URL之后发生的事情
```
【请求阶段】
   *  当用户输入一个域名之后 首先会经过DNS域名解析服务器， 将域名解析成一个公网ip地址 我们可以通过ip地址找到对应的服务器 【每个服务器对应的ip 都是不同的 相当于每个人的身份证】
   *
   *  找到这个服务器之后 我们根据请求的端口号 【端口号也是唯一的】找到服务器当中对应的文件目录 如果有参数或者哈希值的话我们也要进行相对应的计算，服务端解析到参数的值，进行相对应的操作
   *   最后将需要的文件【在服务端当中不是页面，而是源代码】返回给客户端【浏览器】
   *
【渲染阶段】
   *    客户端【浏览器】接受到服务器端的文件之后  首先会计算dom树 紧接着会按照代码从上到下加载 遇到css会形成 style tree 碰到标签会加载dom tree 最后render 集中渲染显示
   *
   *    我们把客户端请求服务端数据的完整的一个过程叫做 http事物
   *    客户端发送的是参数 地址         
    *    服务端返回的是数据文件
    *
    *    注意 当客户端拿到服务器端 返回的源码的时候 进项渲染的时候会碰到标签 link a script img..碰到这些外链的标签 会重新进行数据请求  也会形成一个http事务
    *
    *    这些http请求 会造成页面加载缓慢】
    *
    *    请求头 ：客户端进行设置 服务端获取
    *    响应头 ：服务端进行设置 客户端进行获取
    *
    *    请求体：发送给服务端的代码：例如：post发送 xhr.send（发送的代码）
   *     响应体：服务端返回给客户端的数据 例如：xhr.response xhr.responseText
   *
   *     服务端收到客户端的相应优先会收到客户端的请求头其次是请求体
   *     返回也是一样 客户端优先收到响应头 其次是相应体
   *
【http报文】
   *      客户端和服务器在进行交互的时候，客户端会发送一些参数给服务端，服务端会返回一些数据给客户端，像这样参数和数据内容，我们统称http报文

```
```
【http请求阶段：向服务器发送请求】
1、浏览器根据请求的URL地址，首先向DNS域名服务器发送请求
2、DNS反解析：根据浏览器请求地址中的域名，到DNS服务器中找到对应的服务器外网IP
3、通过找到的外网IP，向对应的服务器发送请求
4、通过URL中的端口号，找到服务器上对应的服务，以及服务所管理的项目源文件

【http响应阶段：服务器把客户端需要的内容准备好，返回给客户端】
5、服务器根据请求地址中的路径名称、问号传参或者哈希值，把客户端需要的内容进行准备和处理
6、把准备的内容响应给客户端（如果请求的是html或者css等文件，服务器返回的是源代码）

【浏览器渲染阶段】
7、客户端浏览器接收到服务器返回的源代码，基于自己内部的渲染引擎（内核）开始页面的绘制和渲染
 =>--首先计算DOM结构，生成DOM tree
 
 --自上而下运行代码，加载css等资源内容
 
 --根据css生成带样式的 render tree
 
 --开始渲染和绘制
 
```
#### 具体的客户端和服务器端交互模型
```
http事务：一次完整的请求+响应

一个页面加载完成，需要向服务器发起很多次http事务操作
一般来说：首先把html源代码拿回来，加载html的时候，遇到link，src，img，script，iframe，video和audio【没有设置preload = ‘none’】等都会重新和服务器端建立http事务交互

特殊情况：如果我们做了资源缓存处理（304），而且即将加载的资源在之前已经加载过了，这样的操作和传统的http事务不同，他们是从服务器和浏览器的缓存中读取数据，比传统的读取快很
```
#### url查询信息和对象之间的互转
```
如何把URL的查询信息变成一个对象
let obj = {};
let url = 'http://www.baidu.com?bbs=123&xx=321';

url = url.substring(url.indexOf('?')+1);
url.split('&').forEach(d=>{
    let arr = d.split('=');
    obj[arr[0]] = arr[1];
});
================================
/*
    {bbs: "123", xx: "321"} -> bbs=123&xx=321
*/

let obj2 = {bbs: "123", xx: "321"};
let arr = [];
for(let attr in obj2){
    arr.push(attr+'='+obj2[attr]);
}
console.log(arr.join('&'));
```


