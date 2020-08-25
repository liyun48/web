# 闭包

有权访问另一个函数作用域中的变量的函数

作用：正常函数执行完毕，声明的变量被垃圾回收处理掉，但闭包可以让作用域里的变量在函数执行完毕后依然保持

形成条件：1. 函数嵌套  2. 内部函数引用外部函数的布局变量

优点：让代码更加规范、简介

缺点：使用闭包过多，导致内存无法释放,从而内存占用过高

应用场景：

​	Ajax请求成功的回调

​	一个事件绑定的回调方法

​	setTimeout的延时回调

​	一个函数内部返回另一个匿名函数

```javascript
function foo () {
    var name = 'terry'
    console.log(name) // terry
    return function () {
        name = 'larry'
        console.log(name) // larry
    }
}
var bar = foo()
bar() // 外部函数访问内部变量
```

例1： 计数器

```javascript
// 
function addCount() {
  var count = 0
  return function() {
    count += 1
    console.log(count)
  }
}
var countResult = addCount()
countResult() // 1
countResult() // 2
countResult() // 3
```

例2：循环打印

```javascript
for (var i = 0; i < 4; i++) {
  setTimeout(function() {
    console.log(i)
  }, 300)
} // 4 4 4 4
// 原因: js执行会先执行主线程，异步相关的会存到异步队列里，当主线程执行完毕开始执行异步队列
// 如何修改使其正常打印: (使用闭包使其正常打印)
for (var i = 0; i < 4; i++){
	setTimeout(
		(function(i) {
            return function(){
            	console.log(i) 
			}
		})(i), 300)
} // 0 1 2 3
for (var i = 0; i < 4; i++) {
  (function(i) {
    setTimeout(function() {
      console.log(i)
    }, 300)
  })(i)
} // 0 1 2 3
```

例3：真实的获取多个元素并添加点击事件

```javascript
var op = document.querySelectorAll("p")
for (var j = 0; j < op.length; j++) {
  op[j].onclick = function() {
    alert(j)
  }
} // 3
for (var j = 0; j < op.length; j++) {
	(function(j) {
  		op[j].onclick = function() {
    		alert(j)
  		}
	})(j)
}
for (var j = 0; j < op.length; j++) {
    op[j].onclick = (function(j) {
      	return function() {
        	alert(j)
		}
	})(j)
}
```

# 原型和原型链

# String方法

#### split()

把一个字符串分割成字符串数组

#### charAt()

返回指定位置的字符

#### toUpperCase()  toLowCase()

toUpperCase() : 把输入字符串中的写大字母全部变成小写字符

toLowCase() : 把输入字符串中的小写字母全部变成大写字符

#### substr()  substring()

substr() : 截取字符串中子串,参数为start索引，length值

substring() : 截取字符串中子串,参数为start索引，end索引

#### toString()

可以将所有的的数据都转换为字符串，但是要排除null 和 undefined

# Array方法

#### join()

把数组中的所有元素放入一个字符串

# 节流函数和防抖函数

节流函数 : 一个需要频繁触发的函数，在规定时间内，只让第一次生效，后面不生效

```javascript
function throttle(fn, delay){
    // 记录上一次函数触发的时间
    var lastTime = 0
    return function(){
        // 记录当前函数触发的时间
        var nowTime = Date.now()
        if(nowTime - lastTime > delay){
            fn()
            // 同步时间
            lastTime = nowTime
        }
    }
}
document.onscroll = throttle(function(){console.log('---')}, 200)
```

防抖函数 : 一个需要频繁触发的函数，在规定时间内，只让最后一次生效，后面不生效

```javascript
function debounce(fn, delay){
    // 记录上一次的延时器
    var timer = null
    return function(){
        // 清除上一次的延时器
    	clearTimeout(timer)
    	// 重新设置新的延时器
    	timer = setTimeout(function(){
        	fn().apply(this)
    	}, delay)
    }
}
document.getElementById('btn').onclick = debounce(function(){console.log('---')}, 1000)

```

# 跨域

同源策略：浏览器安全策略，协议、域名、端口号必须完全一致

跨域：违背同源策略就会产生跨域

解决：jsonp cors 服务器代理 ...