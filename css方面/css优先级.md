#### css优先级排序
```
不同级别：总结排序：!important > 行内样式>ID选择器 > 类选择器 > 标签 > 
通配符 > 继承 > 浏览器默认属性
		1.属性后面加!import 会覆盖页面内任何位置定义的元素样式
		2.作为style属性写在元素内的样式
		3.id选择器
		4.类选择器
		5.标签选择器
		6.通配符选择器（*）
		7.浏览器自定义或继承
	同一级别：后写的会覆盖先写的
```
#### 画三角
```
 #box{
        width:0;
        border:80px solid;
        border-color: transparent transparent red
    }
```
#### display none和visibility hidden区别
```
两者设置的都会使元素隐藏，不可点击

display :none
- 隐藏的元素完全消失，占据的空间也消失，页面会重排；
- 父级设置了none,子级设置block也不管用
visibility:hidden 
- 隐藏的元素消失，但是占据的空间不消失，页面不会重排；
- 父级设置了hidden，子级设置visible管用
```
