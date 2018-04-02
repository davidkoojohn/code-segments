
### Node.js接入层请求后端服务简单的代码实现：

```javascript
exports.example = async (ctx)=>{
  let options = {
    port: 80,
    hostname: 'www.test.com',
    method:'GET',
    path:'/api/getuser?token=document.cookie.token'
  };
  let getData = function (){
    return new Promise((resolve , reject)=>{
      let request = http.request(options , (socket)=>{
        let data = '';
        console.log('status: ' , socket.statusCode , socket.headers);
        socket.on('data' , (chunk)=>{
          data += chunk;
        });
        socket.on('end' , ()=>{
          console.log('server call back get data: ' , data);
          return resolve(data);
        });
        socket.on('error' , (e)=>{
          return reject(data);
        });
      });
      request.end();
    });
  }
  ctx.body = await getData();
}
```

*`from:`https://juejin.im/post/5ac0fc51f265da23970701b9?utm_source=gold_browser_extension*

