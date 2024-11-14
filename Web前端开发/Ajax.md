# Ajax

异步的JavaScript和XML。

作用：

​	数据交换：

​		通过Ajax可以给服务器发送请求，并获取服务器响应的数据

​	异步交互：

​		可以在**不重新加载整个页面**的情况下，**与服务器交换数据并更新部分网页**的技术，如：搜索联想、用户名是否可用的校验等等。

## Ajax原生请求

**一、创建 XMLHttpRequest 对象**

```javascript
let xhr = new XMLHttpRequest();
```

**二、配置请求**

1. 设置请求方法（GET、POST 等）和请求 URL。

```javascript
xhr.open('GET', 'your_url_here', true);
// 或者是 POST 请求
// xhr.open('POST', 'your_url_here', true);
```

1. 如果是 POST 请求，需要设置请求头，指定内容类型。

```javascript
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
```

**三、发送请求**

如果是 GET 请求，直接发送即可；如果是 POST 请求，可以传入要发送的数据作为参数。

javascript

```javascript
// GET 请求
xhr.send();

// POST 请求
xhr.send('key1=value1&key2=value2');
```

**四、处理响应**

1. 通过监听 `onreadystatechange` 事件来处理响应。

```javascript
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 200) {
        // 请求成功，处理响应数据
        let response = xhr.responseText;
        console.log(response);
    } else if (xhr.readyState === 4 && xhr.status!== 200) {
        // 请求失败，处理错误
        console.error('Request failed with status:', xhr.status);
    }
};
```

在上述代码中，`readyState` 表示请求的状态，`status` 表示 HTTP 状态码。当 `readyState` 为 4 且 `status` 为 200 时，表示请求成功，可以获取响应数据。如果状态码不是 200，则表示请求失败。

# Axios

对原生Ajax进行封装，简化书写，快速开发

需要导包

```javascript
<body>
<input type="button" value="获取数据GET"onclick="get()">
<input type="button" value="删除数据GET"onclick="post()">
</body>
<script>
  function get(){
      // 通过axios发送异步请求-get
      axios({
          method:"get",
          url:"https://yapi.pro/mock/572798/user/getById",
          data:"id=1"
      }).then(result=>{
          console.log(result.data)
      })

  }
  function post(){
      // 通过axios发送异步请求-post
      axios({
          method:"post",
          url:"https://yapi.pro/mock/572798/user/deletById",
          data:"id=1"
      }).then(result=>{
          console.log(result.data)
      })
  }
</script>
```

简化

```js
function get() {
    // 通过axios发送异步请求-get
    axios.get("https://yapi.pro/mock/572798/user/getById").then(result => {
        console.log(result.data);
    })

}

function post() {
    // 通过axios发送异步请求-post
    axios.post("https://yapi.pro/mock/572798/user/deletById", "id=1").then(result => {
        console.log(result.data)
    })
}
```

