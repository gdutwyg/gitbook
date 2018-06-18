#  vue-resource与 axios  

**[vue-resource](https://github.com/pagekit/vue-resource)**和 **[axios](https://github.com/mzabriskie/axios)**都是前端的网络请求插件( ajax 插件)，axios是基于 **promise**的，vue-resource是基于 **vue**的插件
不过官方推荐vue2.0使用 **axios**，并不再对 **vue-resource**更新
- axios： Promise based HTTP client for the browser and node.js
- vue-resource：The plugin for Vue.js provides services for making web requests and handle responses using a XMLHttpRequest or JSONP.

下面我基于二者使用过程中发现的一些问题，记录下来，方便以后不要踩坑

1. 因为axios不是vue插件，所以使用不能用vue.use(axios)，那如果我想在vue中使用this.axios.get/post **(注释：vue.use(vue-resource)之后，vue-resource可以直接使用this.$http.get/post)**，应该怎么办？       
**答：**  
    ```javascript
    Vue.prototype.axios = axios  //给vue原型加上axios，方便组件直接使用this.axios
    ```

2. 在IE中会出现promise未定义的情况,这是因为ie并不支持promise的写法，那怎么办？   
**答：** 需要安装 **es6-promise**模块   
    `npm instal es6-promise --save-dev`

    然后在main.js引入，引入后执行它的polyfill方法
    ```
    import es6-promise from 'es6-promise'
    es6-promise.polyfill()
    ```
    或者安装 **babel-polyfill** 模块 && `import 'babel-polyfill'`

3. 使用vue-resource或者axios可能会出现  
    ```
    XMLHttpRequest cannot load xxxxxxxx. Request header field Content-Type is not allowed by Access-Control-Allow-Headers in preflight response.
    ```
 并且Chrome 的网络面板里，这个请求并不是 POST，而是 OPTIONS
 这个因为Content-Type并不被支持；
 发送的请求Content-Type内容类型如果不是 application/x-www-form-urlencoded，multipart/form-data 或 text/plain 这三者的话，便会触发 OPTIONS 请求， axios应该为`application/json`

 解决方法如下：
    - 在 vue-resource 中，我们可以设置 `Vue.http.options.emulateJSON = true`。
    - 在axios第三个参数中设置
    ```
    {headers: {'Content-Type': 'application/x-www-form-urlencoded'}}
    ```
    - 或者
    ```
        var params = new URLSearchParams();
        params.append('param1', 'value1');
        params.append('param2', 'value2');
        axios.post('/foo', params);
    ```
    - 或者[qs](https://github.com/ljharb/qs)
    ```
    var qs = require('qs');
    axios.post('/foo', qs.stringify({ 'bar': 123 }));
    ```
    **参考来自**：https://juejin.im/entry/58eaf351a22b9d0058a8e35c

4. **vue-cli** 使用axios或者vue-resource在开发阶段请求可能会 **涉及跨域**问题，那应该怎么办？ 
webpack配置下有个代理配置模块，在config目录下index.js里面proxyTable里面设置
```
proxyTable: {
  '/operation': {
    target: 'http://192.168.2.79:8000/app/operation',
    changeOrigin: true,
    secure: false,
    pathRewrite: {
      '^/operation': ''
    }
  }       
}
```
即可

5. vue-resource get请求如何传递参数？
```
    答：this.$http.get(url, {params: get参数})
```

6. **未完待续。。。**