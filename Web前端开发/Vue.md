# Vue

Vue是一套前端框架，免除原生JavaScript中的DOM操作，简化书写。

基于MVVM（Model-View-ViewModel）思想，实现数据的双向绑定，将编程的关注点放在数据上。

```vue
// 新建HTML页面，引入Vue.js文件
<script src="../js/vue.js"></script>
<body>
// 编写视图
<div id="app">
    <input type="text" v-model="message">
    {{message}}
</div>
</body>
// 在JS代码区域，创建Vue核心对象，定义数据模型
<script>
    // 定义Vue对象
    new Vue({
        el: "#app", // Vue接管区域
        data: {
            message: "Hello Vue"
        }
    })
</script>
```

## 常用指令

**v-bind**	为HTML标签绑定属性，如设置href，css样式等

**v-model**	为表单元素创建双向数据绑定

```vue
<body>
<div id="app">
    <a v-bind:href="url">链接1</a>
	// v-bind可以省略
    <a :href="url">链接2</a>
	// input框中url改变，a标签里面的url也会跟着改变
    <input type="text" v-model:id="url">
</div>
</body>
<script>
    new Vue({
        el: "#app",
        data: {
            url:"https://www.baidu.com"
        }
    })
</script>
```

注意：通过v-bind或者v-model绑定的变量，必须在数据模型中声明。

**v-on**	为HTML标签绑定事件

```vue
<body>
    <div id="app">
        <input type="button" value="按钮" v-on:click="handle()">
        <input type="button" value="按钮" @click="handle()">
    </div>
</body>
<script>
    new Vue({
        el: "#app",
        data: {

        },
        methods: {
            handle: function () {
                alert('我被点击了');
            }
        }
    })
</script>
```

**v-if**	

**v-else-if**	条件性的渲染某元素，判定为true时渲染，否则不渲染

**v-else**

```vue
<div id="app">
    年龄<input type="text" v-model="age">经判定，为：
    <span v-if="age<=35">年轻人（35周岁以下）</span>
    <span v-else-if="age>35&&age<60">中年人（35-60）</span>
    <span v-else>老年人（60岁以上）</span>
    <br><br>
</div>
</body>
<script>
    new Vue({
        el: "#app",
        data: {
            age: 20
        },
        methods: {

        }
    })
</script>
```

**v-show**	根据条件展示某元素，区别在于切换的是display属性的值

```vue
<body>
<div id="app">
    年龄<input type="text" v-model="age">经判定，为：
    <span v-if="age<=35">年轻人（35周岁以下）</span>
    <span v-else-if="age>35&&age<60">中年人（35-60）</span>
    <span v-else>老年人（60岁以上）</span>
    <br><br>
    年龄<input type="text" v-model="age">经判定，为：
    <span v-show="age<=35">年轻人（35周岁以下）</span>
    <span v-show="age>35&&age<60">中年人（35-60）</span>
    <span v-show="age>=60">老年人（60岁以上）</span>
</div>
</body>
<script>
    new Vue({
        el: "#app",
        data: {
            age: 20
        },
        methods: {}
    })
</script>
```

**v-for**	列表渲染，遍历容器的元素或者对象的属性

```vue
<body>
    <div id="app">
        // index：索引，不需要直接删掉就可以
       	<div v-for="(addr,index) in address">{{index}}:{{addr}}</div>
		<div v-for="addr in address">{{addr}}</div>
    </div>
</body>
<script>
    new Vue({
        el: "#app",
        data: {
            address:['北京','上海','西安','成都','深圳']
        },
        methods: {}
    })
</script>
```

## 案例

通过Vue完成表格数据的渲染展示

```vue
<body>
<div style="font-size: 30px;text-align: center;">成绩单</div>
<div id="app">
    <table width="800px" border="1" cellspacing="0" align="center">
        <tbody>
        <tr>
            <th>编号</th>
            <th>姓名</th>
            <th>年龄</th>
            <th>性别</th>
            <th>成绩</th>
            <th>等级</th>
        </tr>
        <tr align="center" v-for="(stu,index) in students">
            <td>{{index + 1}}</td>
            <td>{{stu.name}}</td>
            <td>{{stu.age}}</td>
            <td>
                <span v-if="stu.gender==1">男</span>
                <span v-if="stu.gender==0">女</span>
            </td>
            <td>{{stu.score}}</td>
            <td>
                <span v-if="stu.score>=85">优秀</span>
                <span v-else-if="stu.score>=60&&stu.score<85">及格</span>
                <span v-else style="color: red">不及格</span>
            </td>
        </tr>
        </tbody>
    </table>
</div>

</body>
<script>
    new Vue({
        el: "#app",
        data: {
            students: [{
                name: "汤姆",
                age: 20,
                gender: 1,
                score: 78
            }, {
                name: "小花",
                age: 18,
                gender: 0,
                score: 90
            }, {
                name: "杰瑞",
                age: 19,
                gender: 1,
                score: 50
            }, {
                name: "张三",
                age: 18,
                gender: 1,
                score: 80
            }, {
                name: "杨幂",
                age: 28,
                gender: 0,
                score: 60
            }, {
                name: "郭德纲",
                age: 69,
                gender: 0,
                score: 59
            }]
        },
        methods: {}
    })

</script>
```

## 生命周期

指一个对象从创建到销毁的整个过程。

生命周期的八个阶段：每触发一个生命周期事件，会自动执行一个生命周期的方法（钩子）

**1. beforeCreate（创建前）**：在实例初始化之后，数据观测和事件配置之前被调用。此时组件的实例刚刚被创建，还不能访问到 `data`、`computed`、`watch` 等属性和方法。

**2. created（创建后）**：实例已经创建完成，属性已经绑定，但是 DOM 还没有挂载，`$el` 属性目前不可见。可以在这里进行一些数据请求和初始化操作。

**3. beforeMount（挂载前）**：在挂载开始之前被调用，此时模板已经编译完成，但还没有渲染到页面中。

**4. mounted（挂载后）**：实例被挂载到 DOM 上后调用，此时可以访问到 DOM 元素，可以进行一些 DOM 操作。

**5. beforeUpdate（更新前）**：数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。

**6. updated（更新后）**：由于数据更改导致的虚拟 DOM 重新渲染和打补丁之后调用。可以执行依赖于 DOM 的操作，但是要注意避免在此期间更改状态，因为这可能会导致无限循环的更新。

**7. beforeDestroy（销毁前）**：实例销毁之前调用。在这一步，实例仍然完全可用，可以在这个阶段进行一些清理操作，比如清除定时器、取消订阅事件等。

**8. destroyed（销毁后）**：实例销毁后调用。此时所有的绑定和实例的指令都已经解绑，所有的子实例也都已经被销毁

```vue
<body>
<div id="app">

</div>
</body>
<script>
    new Vue({
        el: "#app",
        data: {},
        methods: {},
        mounted() {
            alert('Vue挂载完成，发送请求到服务端')
        }
    })
</script>
```

**mounted**：挂载完成，Vue初始化成功，HTML页面渲染成功。（发送数据到服务端，加载数据）

## vue基本使用方法

```vue
<template>
  <div class="hello">
    <!-- 插值表达式：{{  }} -->
    <h1>{{ name }}</h1>
    <h1>{{ age > 60 ? '老年人' : '青年人' }}</h1>
    <!-- 属性绑定：v-bind:value="" 或 :value="" -->
    <div><input type="text" v-bind:value="name"></div>
    <div><input type="text" :value="age"></div>
    <!-- 方法绑定：v-on:XXX="" 或 @XXX -->
    <input type="button" value="保存" v-on:click="handleSave">
    <input type="button" value="修改" @click="changeName">
    <!-- 双向绑定：v-model="" -->
    <input type="text" v-model="name">
    <div><img :src="src"></div>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      name: '刘亦菲',
      age: '保密',
      src: 'https://tse2-mm.cn.bing.net/th/id/OIP-C.84cMrte2f_phgtkL3bU3NAHaNK?rs=1&pid=ImgDetMain'
    }
  },
  methods: {
    handleSave() {
      alert('姓名：' + this.name + '年龄：' + this.age)
    },
    changeName() {
      this.name = 'Liu YiFei'
    }
  }
}
</script>
```

## 解决跨域问题

```js
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  /* 修改前端服务的端口号 */
  devServer: {
    port: 7070,
    /* 配置代理，解决跨域问题 */
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        pathRewrite: {
          '^/api':''
        }
      }
    }
  }
})
```

## axios发送各种请求

```vue
<template>
  <div class="hello">
    <!-- 插值表达式：{{  }} -->
    <h1>{{ name }}</h1>
    <h1>{{ age > 60 ? '老年人' : '青年人' }}</h1>
    <!-- 属性绑定：v-bind:value="" 或 :value="" -->
    <div>姓名：<input type="text" v-bind:value="name"></div>
    <div>年龄：<input type="text" :value="age"></div>
    <!-- 方法绑定：v-on:XXX="" 或 @XXX -->
    <input type="button" value="保存" v-on:click="handleSave">
    <input type="button" value="修改" @click="changeName">
    <!-- 双向绑定：v-model="" -->
    <input type="text" v-model="name">
    <input type="button" value="发送POST请求" @click="handleSendPost">
    <input type="button" value="发送GET请求" @click="handleSendGet">
    <input type="button" value="统一请求方式" @click="handleSend">
    <div><img :src="src"></div>

  </div>
</template>

<script>

import axios from 'axios';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      name: '刘亦菲',
      age: '保密',
      src: 'https://tse2-mm.cn.bing.net/th/id/OIP-C.84cMrte2f_phgtkL3bU3NAHaNK?rs=1&pid=ImgDetMain'
    }
  },
  methods: {
    handleSave() {
      alert('姓名：' + this.name + '年龄：' + this.age)
    },
    changeName() {
      this.name = 'Liu YiFei'
    },
    handleSendPost() {
      // 通过axios发送post请求
      axios.post('/api/admin/employee/login',
        {
          username: 'admin',
          password: '123456'
        }
      ).then(res => {
        console.log(res.data)
      }).catch(error => {
        console.log(error.response)
      }
      )
    },
    handleSendGet() {
      // 通过axios发送get请求
      axios.get('/api/admin/shop/status', {
        headers: {
          token: 'eyJhbGciOiJIUzI1NiJ9.eyJlbXBJZCI6MSwiZXhwIjoxNzMzMTUxMzA5fQ.8J4xKakD_5-ueRrpeHjIDxz79YT9vDGWAypbztXlHSg'
        }
      }
      ).then(res => {
        console.log(res.data)
      }).catch(error => {
        console.log(error.response)
      })
    },
    handleSend() {
      // 使用axios提供的统一调用方式发送请求
      axios({
        url: '/api/admin/employee/login',
        method: 'post',
        data: {
          username: 'admin',
          password: '123456'
        }
      }).then(res => {
        console.log(res.data.data.token)
        axios({
          url: '/api/admin/shop/status',
          method: 'get',
          headers: {
            token: res.data.data.token
          }
        })
      }).catch(error => {
        console.log(error.response)
      });
    }
  }
}
</script>
<style>
</style>
```

## 路由 Vue-Router

> [!NOTE]
>
> **什么是路由？**
>
> 根据浏览器访问的**路径不同**，展示**不同的视图组件**。
>
> **Vue应用中如何实现路由？**
>
> 通过 vue-router 实现路由功能，需要安装js库（**npm install vue-router**）

路由的组成：
VueRouter：路由器，根据路由请求在路由视图中动态渲染对应的视图组件

< router-link>：路由链接组件，浏览器会解析为< a>

< router-view>：路由视图组件，用来展示与路由相匹配的视图组件

router-link 请求 VueRouter 路由表，路由表再更新 router-view 视图

## 路由配置

标签式

```vue
<router-link to="/">Home</router-link> 
```

编程式

```vue
<template>
  <div id="app">
    <nav>
      <input type="button" value="编程式路由跳转" @click="jump">
    </nav>
    <!-- 视图组件展示的位置 -->
    <router-view/>
  </div>
</template>

<script>
export default {
  methods: {
    jump() {
      // 使用编程式路由跳转方式
        this.$router.push('/about')
      }
    }
  }
</script>
<style>
</style>
```

**不存在的请求路径怎么处理？**

配置一个404页面路由

所有不存在的页面请求全部重定向到404页面

```js
import Vue from 'vue'
import VueRouter from 'vue-router'
import HomeView from '../views/HomeView.vue'

Vue.use(VueRouter)

// 维护路由表，某个路由对应的哪个视图组件
const routes = [
  {
    path: '/',
    name: 'home',
    // 静态
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    // 懒加载，项目打包时打包到单独的js文件中，请求时才会加载，性能更好
    component: () => import(/* webpackChunkName: "about" */ '../views/AboutView.vue')
  },
  {
    path: '/404',
    component: () => import('../views/404View.vue')
  },
  {
    path: '*',
    /* 资源不存在重定向 */
    redirect: '/404'
  }
]

const router = new VueRouter({
  routes
})

export default router
```

## 嵌套路由

**安装element-ui**

```
npm i element-ui -S
```

**main.js**

```js
import ElementUI from 'element-ui' 
import 'element-ui/lib/theme-chalk/index.css';

// 全局使用 ElementUI
Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
}).$mount('#app')

```

**index.js**

```js
{
    path: '/c',
    component: () => import('../views/container/ContainerView.vue'),
    // 重定向到指定路由
    redirect: '/c/p1',
    // 嵌套路由（子路由），对应的组件会展示在当前组件内部
    children: [
      {
        path: '/c/p1',
        component: () => import('../views/container/P1View.vue'),
      },
      {
        path: '/c/p2',
        component: () => import('../views/container/P2View.vue'),
      },
      {
        path: '/c/p3',
        component: () => import('../views/container/P3View.vue'),
      },
    ]
  }
```

**ContainerView.vue**

```vue
<template>
    <el-container>
        <el-header>Header</el-header>
        <el-container>
            <el-aside width="200px">
                <router-link to="/c/p1">P1</router-link><br>
                <router-link to="/c/p2">P2</router-link><br>
                <router-link to="/c/p3">P3</router-link><br>
            </el-aside>
            <el-main>
                <router-view></router-view>
            </el-main>
        </el-container>
    </el-container>
</template>
```

**P1\P2\P3.vue**

```vue
<template>
    <div>这是P1 View</div>
</template>
```

## 状态管理 vuex

vuex 是一个专门为Vue.js应用程序开发的状态管理库

vuex 可以在多个组件之间共享数据，并且共享的数据时响应式的，即数据的变更能及时渲染到模板

vuex 采用集中式存储管理所有组件的状态

**安装vuex**

```
npm install vuex@next --save
```

**核心概念**

state：状态对象，集中定义各个组件共享的数据

mutations：类似于一个事件，用于修改共享数据，要求必须是同步函数

actions：类似mutation，可以包含异步操作，通过调用mutation来改变共享数据

**index.js**

```js
import Vue from 'vue'
import Vuex from 'vuex'
import axios from 'axios'

Vue.use(Vuex)

// 集中管理多个组件之间共享的数据
export default new Vuex.Store({
  // 共享数据
  state: {
    name: '未登录用户'
  },
  getters: {
  },
  // 修改共享数据只能通过mutation实现，必须是同步操作
  mutations: {
    setName(state, newName) {
      state.name = newName
    }
  },
  // 通过actions可以调用mutations，在actions中可以进行异步操作
  actions: {
    setNameByAxios(context) {
      axios({
        url: '/api/admin/employee/login',
        method: 'post',
        data: {
          username: 'admin',
          password: '123456'
        } 
      }).then(res => {
        if (res.data.code == 1) {
          // 异步请求后，需要修改共享数据
          // 在actions中调用mutations中定义的setName函数
          context.commit('setName',res.data.data.name)
        }
      })
      }
  },
  modules: {
  }
})
```

**App.vue**

```vue
<template>
  <div id="app">
    <div>欢迎你，{{ $store.state.name }}</div>
    <input type="button" value="通过mutations修改共享数据" @click="handleUpdate"><br>
    <input type="button" value="调用actions中定义的函数" @click="handleCallAction"><br>
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  methods: {
    handleUpdate() {
      // mutations定义的函数不能直接调用，必须通过这种方式来调用
      // setName为mutations中定义的函数，lisi为传递的参数
      this.$store.commit('setName','lisi')
    },
    handleCallAction() {
      this.$store.dispatch('setNameByAxios')
    }
  }
}
</script>
```

**vue.config.js**

```js
const { defineConfig } = require('@vue/cli-service')
module.exports = defineConfig({
  transpileDependencies: true,
  devServer: {
    port: 7777,
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        pathRewrite: {
          '^/api': ''
        }
      }
    }
  }
})
```

## TypeScript

安装TypeScript

```
npm install -g typescript
```

> [!NOTE]
>
> TS为什么要增加**类型支持**？
>
> TS 属于静态类型编程语言，JS属于动态类型编程语言
>
> 静态类型在编译期做类型检查，动态类型在执行期做类型检查
>
> 对于JS来说，需要等到代码执行的时候才能发现错误
>
> 对于TS来说，在代码编译的时候就可以发现错误
>
> 配合VSCode开发工具，TS可以提前到在编写代码的同时就发现代码中的错误，减少找Bug、改Bug的时间

TypeScript是JavaScript的超集，兼容JavaScript

使用tsc命令将ts文件编译成js文件

**常用类型**

| 类型       | 例                                  | 备注                           |
| ---------- | ----------------------------------- | ------------------------------ |
| 字符串类型 | string                              |                                |
| 数字类型   | number                              |                                |
| 布尔类型   | boolean                             |                                |
| 数组类型   | number[],string[],boolean[]依此类推 |                                |
| 任意类型   | any                                 | 相当于又回到了没有类型的时代   |
| 复杂类型   | type 与 interface                   |                                |
| 函数类型   | () => void                          | 对于函数的参数和返回值进行说明 |
| 字面量类型 | "a"\|"b"\|"c"                       | 限制变量或参数的取值           |
| class类    | class Animal                        |                                |

类型标注的位置

​	标注函数

​	标注参数

​	标注返回值

```ts
// 字符串类型
let username: string = 'haust'
// 数字类型
let age: number = 20
// 布尔类型
let isTrue: boolean = true

console.log(username)
console.log(age)
console.log(isTrue)

// 字面量类型
function printText(s:string, alignment: 'left'|'right'|'center') {
    console.log(s,alignment)
}

printText('hello', 'left')

// 接口类型
interface Cat {
    // name后面加上?表示当前属性为可选
    name?: string,
    age: number
}

// 定义变量为Cat类型
const c1: Cat = { name: '小白', age: 1 }
// const c2: Cat = { name: '小白'} 错误：缺少age属性
// const c3: Cat = { name: '小白', age: 1, sex: '公' }    错误：多出sex属性
console.log(c1)

// class类
class User {
    name: string; // 属性
    constructor(name: string) { // 构造方法
        this.name = name
    }
    // 方法
    study() {
        console.log(this.name + '正在学习')
    }
}

const u = new User('张三')

console.log(u.name)
u.study()
```

### 常用类型

```js
// 字符串类型
var username = 'haust';
// 数字类型
var age = 20;
// 布尔类型
var isTrue = true;
console.log(username);
console.log(age);
console.log(isTrue);
// 字面量类型
function printText(s, alignment) {
    console.log(s, alignment);
}
printText('hello', 'left');
// 定义变量为Cat类型
var c1 = { name: '小白', age: 1 };
// const c2: Cat = { name: '小白'} 错误：缺少age属性
// const c3: Cat = { name: '小白', age: 1, sex: '公' }    错误：多出sex属性
console.log(c1);
// class类
var User = /** @class */ (function () {
    function User(name) {
        this.name = name;
    }
    // 方法
    User.prototype.study = function () {
        console.log(this.name + '正在学习');
    };
    return User;
}());
var u = new User('张三');
console.log(u.name);
u.study();
```

### class类-实现接口

```ts
// 定义接口
interface Animal {
    name: string
    eat(): void
}

// 定义一个类实现接口
class Bird implements Animal {
    name: string;
    constructor(name: string) {
        this.name = name
    }
    eat(): void {
        console.log(this.name + 'eat')
    }
}

// 创建类型为Bird的对象
const b1 = new Bird('喜鹊')
console.log(b1.name)
b1.eat()
```

```js
// 定义一个类实现接口
var Bird = /** @class */ (function () {
    function Bird(name) {
        this.name = name;
    }
    Bird.prototype.eat = function () {
        console.log(this.name + 'eat');
    };
    return Bird;
}());
// 创建类型为Bird的对象
var b1 = new Bird('喜鹊');
console.log(b1.name);
b1.eat();
```

### 类的继承

```ts
// 定义一个类，继承上面的类
class Parrot extends Bird {
    say() {
        console.log(this.name + ' say hello')
    }
}

const myParrot = new Parrot('鹦鹉')
console.log(myParrot.name)
myParrot.eat()
myParrot.say()
```

```js
// 定义一个类，继承上面的类
var Parrot = /** @class */ (function (_super) {
    __extends(Parrot, _super);
    function Parrot() {
        return _super !== null && _super.apply(this, arguments) || this;
    }
    Parrot.prototype.say = function () {
        console.log(this.name + ' say hello');
    };
    return Parrot;
}(Bird));
var myParrot = new Parrot('鹦鹉');
console.log(myParrot.name);
myParrot.eat();
myParrot.say();
```

