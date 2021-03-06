# Vuetutor for myself

## 一. vue是什么？vue的模式？什么是MVVM？vue的优点？

### 1. vue 是什么？
- 简单小巧，渐进式，功能强大的技术栈

### 2. vue 的模式？
-  MVVM模式，视图层和数据层的双向绑定，让我们无需再去关心DOM操作的事情，更过的精力放在数据和业务逻辑上去

### 3. 什么是 MVVM ?
MVVM是Model-View-ViewModel的缩写。MVVM是一种设计思想。Model 层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；View 代表UI 组件，它负责将数据模型转化成UI 展现出来，ViewModel 是一个同步View 和 Model的对象。

在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。

ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

### 4. vue的优点？
- 低耦合。视图（View）可以独立于Model变化和修改，一个ViewModel可以绑定到不同的"View"上，当View变化的时候Model可以不变，当Model变化的时候View也可以不变。
- 可重用性。你可以把一些视图逻辑放在一个ViewModel里面，让很多view重用这段视图逻辑。
- 独立开发。开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计。
- 可测试。界面素来是比较难于测试的，而现在测试可以针对ViewModel来写
易用灵活高效

## 二. 数据绑定、指令事件与过滤器
### 1.vue实例和数据绑定
- 1.  <script src="https://cdn.bootcss.com/vue/2.5.17-beta.0/vue.min.js"></script>
通过构造函数 Vue 就可以创建一个 Vue 的根实例，并启动 Vue 应用---入口
```
var app ＝new Vue({
el:'   ',
data:{  }
})
```
- 2. 必不可少的一个选项就是 el 。 el 用于指定一个页面中己存在的 DOM 元素来挂载 Vue实例,可以是标签,也可以是css语法
- 3.  通过 Vue 实例的 data 选项，可以声明应用内需要双向绑定的数据。建议所有会用到的数据都预先在 data 内声明，这样不至于将数据散落在业务逻辑中，难以维护,也可以指向一个已经有的变量
- 4.  挂载成功后我们可以通过app.$el访问元素

Vue 提供了很多常用的实例属性与方法，都以$开头 
```
app.$el, app.$data
```
 vue本身的实例本身也代理了data对象里的所有属性，所以可以这样访问 data元素的属性,直接app.属性名
```
app.msg
```
### 2. 文本插值和表达式
- 在｛｛｝｝中，除了简单的绑定属性值外，还可 以使用 JavaScript 表达式进行简单的运算,三元运算等
---实例
**vue.js 只支持单个表达式，不支持语句和流控制。**
```
{{ 6+6 *3}}---可以进行简单的运算
{{ 6<3 ? msg :a}}---可以用三元运算符 
{{if(6>3){}}-----注意：文本插值的形式，其中不能书写表达式,支持单个表达式
{{var a = 6}}--也是多行表达式   =  > (var a ;a = 6;)
〈！一不能使用流控制，要使用三元运算 一〉
{{ if (ok) return msg ))
```
### 3. 指令和事件


> 指令（ Directives ）是 Vue 模板中最常用的一项功能，它带有前缀 v－，能帮我们
快速完成DOM操作。循环渲染。显示和隐藏
本节目标 v-text , v-html , v-bind , v-on
v-­text:—————­解析文本 和{{ }} 作用一样
v-­html:————— 解析html
v­-bind—————–v­bind 的基本用途是动态更新 HTML 元素上的属性，比如 id 、
class 等,可以简写为  「  ：」 
v­-on——————它用来绑定事件监听器，可以简写为  「 @ 」 

> v­-on具体介绍
在普通元素上， v­on 可以监听原生的 DOM 事件，除了 click 外，还有
dblclick、 keyup, mousemove 等。表达式可以是一个方法名，这些方法都
写在 Vue 实例的 methods 属性内，并且是函数的形式，函数内的 this 指向
的是当前 Vue 实例本身，因此可以直接使用 this.xxx 的形式来访问或修改数
据
**vue中用 到的所有方法都定义在methods中**

### 4. 过滤器

> Vue. 支持在｛｛｝｝插值的尾部添加一小管道符 “ | ” 对数据进行过滤，经常用于格
式化文本，比如字母全部大写、货币千位使用逗号分隔等。过滤的规则是自定义
的， 通过给 Vue 实例添加选项 filters 来设置
过滤器：{{ data | filter | filter}}
{{date | formatDate(a,b)}} 中的第一个和第二个参数
分别对应过滤器的第二个和第三个参数

## 三. 计算属性
### 计算属性（减少模板{{}}的复杂度）
* 基础例子1
* 计算属性的两种写法
```
						computed
<div id="app">
   {{fullName}}
</div>

new Vue({
  el: "#app",
  data: {
  		firstName:'Ji',
   	 	lastName:'RenGu'
  },
 	computed:{
  	fullName(){
    	return this.firstName+'----'+this.lastName;
    }
  }
})
```
* 计算缓存vs方法(Methods)
    * 计算属性computed具有缓存，而methods无缓存
* Computed属性vs 侦听器(Watch属性)
    * watch方法--观察Vue实例上的数据变动,只要指定的数据改变就会执行预定的函数
```
    			watch
    <div id="app">
        {{msg}} <br> 
        改变了吗? {{isChange}}
        <button @click="change">改变</button>
    </div>
    
    new Vue({
      el: "#app",
      data: {
            msg:'欲穷千里目',
          isChange:'No'
      },
        watch:{
        //只要msg改变,这个方法就会执行
        msg(val,oldVal){
            this.isChange = 'Yes'
        }
      },
      methods:{//不得不说ES6写起来真爽
        change(){
            this.msg = '更上一层楼'
        }
      }
    })
```
    * computed方法
* 计算setter 和getter
    * get和set,顾名思义,一个是获得,一个是设置,常规上来讲,计算属性中都是有get和set方法的,默认是只有getter方法,如果需要的话,自然,你也可以写一个setter方法.来个例子,诸位往下看:
   
```						
<div id="app">
 此时的onpiece: {{onepiece}} <br>
 此时的msg:  {{msg}} <br><br>
  <button @click="setName">设置name</button>
</div>		

new Vue({
  el: "#app",
  data: {
  	name:'Kobe',
    msg:''
  },
  methods:{
  	setName(){
    	this.onepiece = 'JorDan'
    }
  },
  computed:{
  	onepiece:{
        get(){
          return this.name +'Bryant';
        },
        set(newVal){
          //当你给onepiece设置值的时候set就就会调用
          this.msg = newVal+'is the greatest basketball player';
        }
    }
  }
})
```