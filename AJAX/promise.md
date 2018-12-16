#### 概念
```
Promise是ES6的新增加的内置类构造函数，目的是管理异步操作的，
用Promise主要是换种写法而已
也叫“Promise”设计模式
Promise本身是同步的，
只是用来管理异步编程的一种模式
new Promise（）创建类的一个实例，每一个实例都可以管理一个异步操作
```
#### 特点
```
有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。
```
#### promise三种状态
```
pending（准备状态：初始化成功，开始执行异步的任务）

fulfilled（成功状态，已经成功）

rejected（失败状态，已经失败）

最终只有两个状态，1、准备 2、成功或者失败
```
#### 基本语法（用法）
```
Promise两个参数：
* resolve：当异步操作执行成功，执行的方法

* reject：当异步操作执行失败，执行的方法

Promise实例生成后，用then方法指定resolved状态和rejected状态的回调函数
其中then方法可以写多个
```
```
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});

promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```
#### 小demo
```
new Promise((resolve,reject)=>{
    // 执行一个异步任务
    //（new Promise时候 创建一个Promise实例，会立即执行这个函数）
    setTimeout(()=>{
        resolve(100);
    },1000)
}).then(()=>{//继续做什么事情
    //第一个传递的函数resolve
    console.log('ok');
},()=>{
    //第二个传递的函数reject
     console.log('error');
});

/*
1、异步操作放在Promise传的函数里面
2、Promise的参数与 then的参数相对应
*/
```
==============================
```
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, ms, 'done');
  });
}

timeout(100).then((value) => {
  console.log(value);
});
```
========================
```
 let a = 10;

    let p = new Promise((resolve,reject)=>{
        setTimeout(()=>{
            a = 20;
        resolve(a);
        },1000);
    });
    p.then((a)=>{
        //成功
        console.log(a);//20
    },()=>{
        //失败
    });
    console.log(a);//10
```
#### Promise来管理异步操作（其中then可以写多个）
```
let pro = new Promise((resolve,reject) =>{
    //执行一个异步操作
    let xhr = new XMLHttpRequset();
    xhr.open('get','1.js',true);
    xhr.onreadyStatechange() = function(){
        if(xhr.readyState === 4 && xhr.status === 200){
            val = xhr.responseText;
            resolve(val);//成功
        }
        if(xhr.status!==200){
            reject();//失败
        }
    }
    xhr.send();
})
pro.then((resolve)=>{
    console.log('ok');
    //数据绑定
},(reject)=>{
    console.log('error');
}).then(()=>{
    //当第一个then中的函数执行完，会执行第二个
}).then(()=>{
     //当第二个then中的函数执行完，会执行第三个
})

```
#### 用Promise解决回调地狱问题(连续运动问题)
```
 div.onclick = function(){
        move({
            ele:div,
            attrs:{
                width:200
            },
            fx:'elasticOut',
            duration:500,
            cb(){
                move({
                    ele:div,
                    attrs:{
                        height:620
                    },
                    duration:500,
                    fx:'elasticOut',
                    cb(){
                        move({
                            ele:div,
                            attrs:{
                                left:300
                            },
                            duration:400,
                            fx:'backBoth',
                            cb(){
                                move({
                                    ele:div,
                                    attrs:{
                                        top:300
                                    },
                                    duration:400,
                                    fx:'bounceOut',
                                }) 
                            }
                        })   
                    }
                })   
            }
        })  
    
        
下面用promise解决


        let m = new Promise((resolve)=>{
            move({
                ele:div,
                attrs:{
                    width:200
                },
                fx:'elasticOut',
                duration:500,
                cb(){
                    resolve();
                }
            })
        })
        .then(()=>{
            return m2 = new Promise((resolve)=>{
                move({
                    ele:div,
                    attrs:{
                        height:620
                    },
                    duration:500,
                    fx:'elasticOut',
                    cb(){
                        resolve();
                    }
                })
            }) })
        .then(()=>{
           return  new Promise((resolve)=>{
                move({
                    ele:div,
                    attrs:{
                        left:300
                    },
                    duration:400,
                    fx:'backBoth',
                    cb(){
                        resolve();
                    }
                })   
            }) })
        .then(()=>{
            move({
                ele:div,
                attrs:{
                    top:300
                },
                duration:400,
                fx:'bounceOut',
                cb(){
                    console.log('完');
                }
            }) 
        })
        // console.log(m);
    }

```
#### 事件循环
```

主任务队列
等待任务队列分为，宏任务和微任务

1.宏任务：包括整体代码script，setTimeout，setInterval；

2.微任务：Promise，process.nextTick


优先执行主任务，主任务执行完（为空），执行微任务(then，按顺序走的)，
微任务执行完之后，开始执行宏任务，按照条件的先后顺序执行，
这种循环的机制就叫事件循环（event loop）
```
```
let p = new Promise((resolve)=>{
    console.log(1);
    resolve(6);
});
let p2 = new Promise((resolve)=>{
    resolve(7);
});
p2.then(e=>{
    console.log(7);
})
console.log(4);
setTimeout(()=>{
    console.log(2);
});
p.then(e=>{
    console.log(e);
});
console.log(5);
setTimeout(()=>{
    console.log(3);
},10);

// 1457623
```