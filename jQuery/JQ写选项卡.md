####  注意点
```
可以链式操作
sibilings('div')
sibilings('button')

index()          默认以父级为基准，找到子级的索引。
index('button')相对于一堆button里面的索引

```
#### 代码
```
 <button class="active">one</button>
    <button>two</button>
    <button>three</button>
    <div class="show">111</div>
    <div>222</div>
    <div>333</div>
    
  $('button').click(function(){
        $(this).addClass('active')
        .siblings('button').removeClass('active');

        $('div').eq($(this).index()).addClass('show')
        .siblings('div').removeClass('show')
        
    })
```