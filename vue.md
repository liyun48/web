#### webpack

​	静态模块打包器   分析代码，转换代码，编译代码，输出代码

​	提供了友好的模块化支持，以及代码压缩混淆，处理js兼容问题，性能优化，提高开发效率和项目的可维护性

​	当 webpack 处理应用程序时,它会递归地构建一个依赖关系图(dependency graph),其中包含应用程序需要的每个模块,然后将所有这些模块打包成一个或多个 bundle。

​	缺点：只能用于采用模块化开发的项目

​	核心：

​			入口：指示webpack应该使用哪个模块来作为构建其内部依赖图的开始

​			输出：告诉webpack在哪里输出它所创建的bundles，以及如何命名这些文件，默认./dist

​			loder：可以将所有类型的文件转换为webpack能够处理的有效模块，然后利用webpack的打包能力对他们进行处理   （模块加载时的预处理文件）

​			插件：解决loader无法实现的其他事。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量

​	模块热替换

​			在运行程序过程中替换、添加、删除模块，而无需重新加载整个页面

​			主要通过一下几种方式来显著加快开发速度：

​				保留在完全重新加载页面时丢失的应用程序状态

​				只更新变更内容，以节省宝贵的开发时间

​				调整样式更加快速

#### http https

1. https协议需要到ca申请证书，一般免费证书较少，因而需要一定费用
2. http是超文本传输协议，信息是明文传输；https则是具有安全性的ssl加密传输协议
3. http和https使用的是完全不同的连接方式，用的端口也不一样，前者是80，后者是443
4. http的连接很简单，是无状态的；https协议是由SSL+HTTP协议构建的可进行加密传输、身份认证的网络协议，比http协议安全

####  HTTP常用状态码

1xx	指示信息 -- 表示请求已接收，继续处理

2xx	成功 -- 表示请求已被成功接收、理解、接受

3xx	重定向 -- 要完成请求必须进行更进一步的操作

4xx	客户端错误 -- 请求有语法错误或请求无法实现

5xx	服务器端错误 -- 服务器未能实现合法的请求

#### vue性能优化

​	使用cdn,不要打包一些公共的文件和组件库

#### Promise

​	是异步编程，用于封装异步代码

​	有三种状态： 进行中（Pending）    成功后（Resolved）   失败后（Rejected）

​	成功  resolve

​	失败  reject

​	Promise实例生成后，使用then方法分别指定resolve状态和rejected状态的回调函数，then方法可以接受两个回调函数作为参数，第一个回调函数是promise对象的状态变为resolved的时候调用，第二个回调函数是promise对象的状态变为rejected时调用。

```javascript
var p = new Promise((resolve,reject)=>{
	setTimeout(()=>{
		let random = Math.random()
        if(random>0.5){
            // 承诺成功
            resolve(random)
        }else{
            // 承诺失败
            reject(random)
        }
	},1000)
})
p
.then((data)=>{
    // 承诺兑现时执行
    console.log(data)
})
.catch((error)=>{
    // 承诺异常时执行
    console.log(error)
})
.finally(()=>{
    // 无论如何都需要执行
})
```

接收多个承诺对象

```javascript
Promise.all([p1, p2,p3], function(){})
// 将p1,p2,p3合并为一个承诺对象,当p1,p2,p3都成功时，p的状态才会转换为成功状态，但如果p1,p2,p3中有一个是失败状态，p的状态就转换为失败状态
Promise.race([p1, p2,p3], function(){})
// p状态与p1,p2,p3中状态改变最快的承诺对象保持一致
```

#### 创建ajax的过程

1. 创建XMLHttpRequest对象，也就是创建一个异步调用对象

2. 创建一个新的HTTP请求，并指定该HTTP请求的方法、URL以及验证信息

3. 设置响应HTTP状态变化的函数

4. 发送HTTP请求

5. 获取异步调用返回的数据

6. 使用javascript和DOM实现局部刷新

   ```javascript
   // 第一步：创建异步对象
   let xhr = new XMLHttpRequest()
   // 第二步：设置请求的url参数
   xhr.open('get', '/baidu.com?username=1')
   // 第三步：设置发送的数据，开始和服务器交互
   xhr.send()
   // 第四步：注册事件onreadystatechange，当状态改变时会调用
   xhr.onreadystatechange = function(){
       if(xhr.readyState === 4 && xhr.status === 200){
           // 第五步：数据返回
           console.log(xhr.responentText)
       }
   }
   ```

优点

1. 页面无需刷新，在页面内与服务器通信
2. 使用异步的方式与服务器通信，不需要中断操作
3. 把以前服务器负担的工作转嫁给客户端，减轻服务器和宽带，可以最大程度减少冗余请求
4. 基于标准化的并被广泛支持的技术，不需要下载插件或者小程序

缺点

1. Ajax干掉了back和history功能，即对浏览器机制的破坏
2. 安全问题，易受到黑客攻击
3. 对搜索引擎的支持比较弱。如果使用不当，AJAX会增大网络数据的流量，从而降低整个系统的性能
4. 不能很好的支持移动设备
5. 违背URL和资源定位的初衷

#### GET POST

1. GET从服务器获取数据，POST向服务器发送数据
2. GET传输数据通过url请求，用？连接,传递信息的数量有限制，一般是2000个字符；POST一般修改服务器上的资源，可以发送大的文件
3. GET 使用Request.QueryString获取变量的值；POST通过Request.Form来获取变量的值

#### MVC MVVC MVVM

`MVC`: Model（数据层，负责存储数据）- View（展现层，用户所看到的页面）- Controller（协调层，负责协调Model和View）

1. `View` 传送指令到 `Controller`
2. `Controller` 完成业务逻辑后，要求 `Model` 改变状态
3. `Model` 将新的数据发送到 `View`，用户得到反馈
4. 所有通信都是单向的

`MVVC`: Model（数据层，负责存储数据）-View（展现层，创建需求创建cell）-View（定义数组，用来接收控制中的数据、处理回调）-Controller（加载网络数据、懒加载）

`MVVM`: Model（数据层，负责存储数据）- View（ViewController层，他的任务就是从ViewModel层获取数据，然后显示）- ViewModel（View和Model层的粘合剂，封装业务逻辑处理，封装网络处理，封装数据缓存。就是把原来ViewController层的业务逻辑和页面逻辑等剥离出来放到ViewModel层）

1. 各部分之间的通信是双向的
2. view的变动自然反应在ViewModel，反之亦然
3. 通过双向数据绑定把View层和Model层连接起来

#### vue中 v-if v-show 区别

v-show 仅仅控制元素的显示方式，将 display 属性在 block 和 none 来回切换。用于切换某个元素的显示/隐藏

而v-if会控制这个 DOM 节点的存在与否。当只需要一次显示或隐藏时，使用v-if更加合理

#### vue生命周期

​	beforeCreate

​	created

​	beforeMount

​	mounted

​	beforeUpdate

​	updated

​	beforeDestory

​	destoryed

#### vue中 computed watch 区别

​	计算属性使用：一个数据属性在它所依赖的属性发生变化时，也要发生变化

​	监听： 当数据发生变化时，执行异步操作或较大开销操作的情况

​	**watch**擅长处理的场景：**一个数据影响多个数据**

​	**computed擅**长处理的场景：**一个数据受多个数据影响**

#### vue react区别

#### vuex

vue状态管理模式

vuex核心：

​	state	状态初始值

​	getter 	加工之后给到外界

​	mutation  处理state数据，同步

​	action  异步操作

​	modules  模块化状态管理

使用方法

​	mapState mapGetters mapMutations MapActions

​	this.$store

​		this.$store.dispatch	含有异步操作，例如向后台提交数据，写法： `this.$store.dispatch('action方法名',值)`

​		this.$store.commit	同步操作，写法：`this.$store.commit('mutations方法名',值)`

#### 组件通信

组件关系：父子 兄弟 隔代

通信方式：

1. props   父传子
2. 自定义事件   $emit   $on
3. slot
4. vuex
5. $praent $children
6. ref

#### $router $route

1. router是VueRouter的一个对象,通过Vue.use(VueRouter)和VueRouter构造函数得到一个router的实例对象，这个对象中是一个全局的对象，他包含了所有的路由包含了许多关键的对象和属性。
2. route是一个跳转的路由对象，每一个路由都会有一个route对象，是一个局部的对象，可以获取对应的name,path,params,query等

#### vue双向绑定的原理和缺点

利用了 `Object.defineProperty()` 这个方法重新定义了对象获取属性值(get)和设置属性值(set)的操作来实现的。

它接收三个参数，要操作的对象，要定义或修改的对象属性名，属性描述符。

`vue` 实现数据双向绑定主要是：采用数据劫持结合发布者-订阅者模式的方式，通过 `Object.defineProperty()` 来劫持各个属性的 `setter`，`getter`，在数据变动时发布消息给订阅者，触发相应监听回调

缺点： 由于各个数据相互依赖相互绑定，导致数据问题的源头难以被跟踪到，子组件修改父组件，兄弟之间相互修改有违设计原则。

#### 虚拟DOM介绍

​	用js模拟DOM结构

​	将DOM对比操作，放在JS层，提高效率

​	虚拟DOM的目的是将所有操作累加起来，统计计算出所有的变化后，统一更新一次DOM

#### vue  jQuery 区别

jQuery专注视图层，通过操作DOM去实现页面的一些逻辑渲染；vue专注数据层，通过数据的双向绑定最终表现在DOM层，减少了DOM的操作

Vue使用了组件化思想，使得项目子集职责清晰，提高了开发效率，方便重复利用，便于协同开发

#### vue-router

​	vue.js的路由管理器

​	`<router-link>`

​		路由跳转

​	`<router-view>`

​		对应页面变化

​	`<keep-alive>`

​		keep-alive 是 Vue 内置的一个组件，可以使被包含的组件保留状态，避免重新渲染 

​		一般结合路由和动态组件一起使用，用于缓存组件，包含router-view

​	**动态路由** 

​		path中冒号后拼接id   

​		通过this.$route.params获取参数

​		响应路由参数的变化   使用watch

​	**vue的路由使用步骤**

​		1.下载vue-router路由模块；

​		2.创建路由对象；

​		3.配置路由规则；

​		4.将路由对象注册为vue实例对象的成员属性；

​	**vue路由的两种模式**

​		hash ——即地址栏URL中的#符号

​		history ——利用了HTML5 History Interface 中新增的pushState() 和replaceState() 方法。

​		可以用model属性切换路由模式

#### vue-loader

基于webpack的一个loader，解析和转换.vue文件，提取出其中的逻辑代码script、样式代码css、以及HTML模板template，再分别把他们交给对应的Loader处理，核心的作用就是提取

webpack的loader： 用来打包、转译js、css文件，把代码转换成浏览器能识别的，还有一些打包、压缩的功能。

#### vue中created和mounted的区别

created： 在模板渲染成html前调用，即通常初始化某些属性值，然后在渲染成视图

mounted： 在模板渲染成html后调用，通常是初始化页面完成后，在对html的dom节点进行一些需要的操作

#### vue 自定义指令

directive

​	全局:

```javascript
Vue.directive('',{
    inserted: function(el){
        console.log(el)
    }
})

```

​	局部:

```js
directives: {
	demo: {
		inserted: function(el) {
			console.log(el)
		}
	}
}

```

钩子函数及参数

```javascript
// 一个指令定义对象可以提供如下钩子函数
bind: function(el,binding,vnode){
    // 指令第一次绑定到元素时调用，只调用一次
    // 在这里可以进行一次性的初始化设置
},
inserted: function(){
    // 被绑定元素插入父节点时调用
},
update: function(oldVnode){
    // 指令所在组件的VNode更新时调用，但是可能发生在其子VNode更新之前
},
componentUpdated: function(){
    // 指令所在组件的VNode及其子VNode全部更新后调用
},
unbind: function(){
    // 只调用一次，指令与元素解绑时调用
}
// 钩子函数参数
/**
 * el:
 * 	指令所绑定的元素，可以用来直接操作DOM，
 *  可修改（其他参数仅可读）
 * binding:
 * 	一个对象，包含以下property:
 * 		name: 指令名，不包含v-前缀
 * 		value: 指令的绑定值
 * 		oldValue: 指令绑定的前一个值，仅在update和componentUpdated钩子中可用。无论值是否改变都可用
 * 		expression: 字符串形式的指令表达式
 * 		arg: 传给指令的参数，可选
 * 		modifiers: 一个包含修饰符的对象
 * vnode: Vue编译生成的虚拟节点
 * oldVnode: 上一个虚拟节点，仅在update和componentUpdated钩子中可用
 */

```

#### Vue 组件 data 为什么必须是函数

如果data是一个对象，那么由于对象本身属于引用类型，修改其中一个属性时，会影响所有Vue实例的数据。

如果data作为一个函数返回一个对象，那么每一个实例的data属性都是独立的，不会相互影响了。

#### vue 自定义过滤器

filter

```html
<div>
    {{msg | demo}}
</div>

```

全局：

```javascript
Vue.filter('', function(value){
    return 
})

```

局部：

```javascript
filters: {
	demo: function(value){
        return
    }
}

```

#### Vue中key的作用

​	key是为Vue中的vnode标记的唯一id，通过这个key，我们的diff操作可以 更准确、更快速

​	为了在diff算法执行时更快的找到对应的节点，提高diff速度

​	key具有唯一性

​	用于管理可复用的元素

#### vue中的事件修饰符

​	.prevent() 阻止默认事件；

​	.once() 只执行一次；

​	.stop() 阻止冒泡；

#### 路由懒加载

​	路由懒加载是通过异步的方式来加载对应的路由组件，提高页面相应速度

#### vue中有哪些内置组件

component slot  transtion fliters