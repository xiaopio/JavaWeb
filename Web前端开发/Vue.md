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