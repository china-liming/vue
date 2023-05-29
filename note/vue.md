# 第1章：Vue核心

## 1.1. Vue简介

### 1.1.1. 官网

1. ​    英文官网：https://vuejs.org/
2. ​    中文官网：https://cn.vuejs.org/



### 1.1.2. 介绍与描述

1. 动态构建用户界面的 <font color="red">渐进式</font> JavaScript框架。
2. 作者：尤雨溪。



### 1.1.3. Vue的特点

1. 遵循 <font color="red">MVVM</font> 模式。
2. 编码简洁，体积小，运行效率高，适合移动/PC端开发。
3. 它本身只关注UI，也可以引入其他第三方库开发项目。



## 1.2. 初识Vue

​	1.想让vue工作，就必须创建一个vue实例，且要传入一个配置对象；

​    2.root容器里的代码依然符合html规范，只不过混入了一些特殊的vue语法；

​    3.root容器里的代码被称为【vue模板】；

​    4.Vue实例和容器是一一对应的；

​    5.真实开发中只有一个Vue实例，并且会配合着组件一起使用；

​    6.{{xxx}}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性；

​    7.一旦data中的数据发生改变，那么页面中用到该数据的地方也会自动更新。

​	注意区分：js表达式 和 js代码(语句)

​    	 1.表达式：一个表达式会产生一个值，可以放在任何一个需要值得地方：

​     		 (1). a

​     		 (2). a + b

​     		 (3). demo(1)

​      		(4). x === y ? 'a' : 'b'

​    	 2.js代码(语句)

​    		  (1). if() {}

​    		  (2). for() {}

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>初识vue</title>
    <!-- 引入vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
  </head>
  <body>
    <!-- 
      初识Vue:
        1.想让vue工作，就必须创建一个vue实例，且要传入一个配置对象；
        2.root容器里的代码依然符合html规范，只不过混入了一些特殊的vue语法；
        3.root容器里的代码被称为【vue模板】；
        4.Vue实例和容器是一一对应的；
        5.真实开发中只有一个Vue实例，并且会配合着组件一起使用；
        6.{{xxx}}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性；
        7.一旦data中的数据发生改变，那么页面中用到该数据的地方也会自动更新。

        注意区分：js表达式 和 js代码(语句)
          1.表达式：一个表达式会产生一个值，可以放在任何一个需要值得地方：
            (1). a
            (2). a + b
            (3). demo(1)
            (4). x === y ? 'a' : 'b'
          2.js代码(语句)
            (1). if() {}
            (2). for() {}
     -->
    
    <!-- 准备好一个容器 -->
    <div id="root">
      <h1>Hello,{{name.toUpperCase()}},{{address}}</h1>
    </div>

    <script type="text/javascript">
      Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示。

      //创建Vue实例
      new Vue({
        el: '#root',  //el用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符串。也可以写为document.getElementById('root')
        data: { //data中用于存储数据，数据供el所指定的容器去使用，值我们暂时先写成一个对象。
          name: 'Vue',
          address: '西安'
        }
      });

    </script>
  </body>
</html>
```



![初识vue](.\img\初识vue.jpg)



## 1.3. 模板语法

Vue模板语法有2大类：

​    1.插值语法：

​     功能：用于解析标签体内容。

​     写法：{{xxx}}，xxx是js表达式，且可以直接读取到data中的所有属性。

​    2.指令语法：

​     功能：用于解析标签(包括：标签属性、标签体内容、绑定事件......)。

​     举例：v-bind:href="xxx" 或 简写为 :href="xxx", xxx同样要写js表达式。

​        且可以直接读取到data中的所有属性。

​     备注：Vue中有很多的指令，且形式都是：v-????. 此处我们只是拿v-bind来举个例子。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>模板语法</title>
    <!-- 引入vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
  </head>
  <body>
    <!-- 
      Vue模板语法有2大类：
        1.插值语法：
          功能：用于解析标签体内容。
          写法：{{xxx}}，xxx是js表达式，且可以直接读取到data中的所有属性。
        2.指令语法：
          功能：用于解析标签(包括：标签属性、标签体内容、绑定事件......)。
          举例：v-bind:href="xxx" 或 简写为 :href="xxx", xxx同样要写js表达式。
                且可以直接读取到data中的所有属性。
          备注：Vue中有很多的指令，且形式都是：v-????. 此处我们只是拿v-bind来举个例子。
    -->


    <!-- 准备好一个容器 -->
    <div id="root">
      <h1>差值语法</h1>
      <h3>你好,{{name}}</h3>
      <hr>
      <h1>指令语法</h1>
      <a v-bind:href="school.url.toUpperCase()" target="_blank" x="hello">点我去学习{{school.name}}1</a>
      <a :href="school.url" target="_blank" :x="name">点我去学习{{school.name}}2</a>
    </div>

    <script type="text/javascript">
      Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示。
      new Vue({
        el: '#root',
        data: {
          name: 'jack',
          school: {
            name: 'vue',
            url: 'https://vuejs.zcopy.site/v2/guide/'
          }
        }
      });
    </script>
  </body>
</html>
```



![模板语法](.\img\模板语法.jpg)



## 1.4. 数据绑定

Vue中有2中数据绑定的方式：

​    1.单向绑定(v-bind)：数据只能从data流向页面。

​    2.双向绑定(v-model)：数据不仅能从data流向页面，还可以从页面流向data。

​     备注：

​      1.双向绑定一般都应用在表单类元素上(如；input、select等)

​      2.v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>数据绑定</title>
    <!-- 引入vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
  </head>
  <body>
    <!-- 
      Vue中有2中数据绑定的方式：
        1.单向绑定(v-bind)：数据只能从data流向页面。
        2.双向绑定(v-model)：数据不仅能从data流向页面，还可以从页面流向data。
          备注：
            1.双向绑定一般都应用在表单类元素上(如；input、select等)
            2.v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。
     -->

    <!-- 准备好一个容器 -->
    <div id="root">
      <!-- 普通写法 -->
      单向数据绑定：<input type="text" v-bind:value="name"><br>
      单向数据绑定：<input type="text" v-model:value="name"><br>

      <!-- 简写 -->
      单向数据绑定：<input type="text" :value="name"><br>
      单向数据绑定：<input type="text" v-model="name"><br>

      <!-- 如下代码是错误的，因为v-model只能应用在表单类元素（输入类元素）上 -->
      <!-- <h2 v-model:x="name">你好啊</h2> -->
    </div>

    <script type="text/javascript">
      Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示。

      new Vue({
        el: '#root',
        data: {
          name: 'vue'
        }
      });
    </script>
  </body>
</html>
```

![数据绑定](.\img\数据绑定.jpg)



## 1.5. el与data的两种写法

data与el的2种写法

​    1.el有2种写法

​     (1).new Vue时候配置el属性。

​     (2).先创建Vue实例，随后再通过vm.$mount('#root')指定el的值。

​    2.data有2种写法

​     (1).对象式

​     (2).函数式

​     如何选择：目前哪种写法都可以，以后学习到组件时，data必须使用函数式，否则会报错。

​    3.一个重要的原则：

​     由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例了。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>数据绑定</title>
    <!-- 引入vue -->
    <script type="text/javascript" src="../js/vue.js"></script>
  </head>
  <body>
    <!-- 
      data与el的2种写法
        1.el有2种写法
          (1).new Vue时候配置el属性。
          (2).先创建Vue实例，随后再通过vm.$mount('#root')指定el的值。
        2.data有2种写法
          (1).对象式
          (2).函数式
          如何选择：目前哪种写法都可以，以后学习到组件时，data必须使用函数式，否则会报错。
        3.一个重要的原则：
          由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例了。
     -->
    <div id="root">
      <h1>你好,{{name}}</h1>
    </div>

    <script type="text/javascript">
      Vue.config.productionTip = false;//设置为 false 以阻止 vue 在启动时生成生产提示。

      // el的两种写法
      /* const v = new Vue({
        el: '#root', //第一种写法
        data: {
          name: 'vue'
        }
      });
      console.log(v);
      v.$mount('#root'); //第二种写法 */

      //data的两种写法
      new Vue({
        el: '#root',
        //data的第一种写法：对象式
        /* data: {
           name: 'vue'
        } */

        //data的第二种写法，函数式
        data() {
          console.log('@@@', this)//此处的this是Vue实例对象
          return {
            name: 'vue'
          }
        }
      });
    </script>
  </body>
</html>
```

![el与data的两种写法](.\img\el与data的两种写法.jpg)



## 1.6 MVVM模型

1. M：模型（Model）：对应data中的数据
2. V：视图（View）：模板
3. VM：视图模型（ViewModel）：Vue实例对象

![MVVM模型](.\img\MVVM模型.jpg)