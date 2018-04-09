## wx.request自己封装一个基于promise的异步请求方法

```javascript
// wx.request的一个官方示例代码
wx.request({
  url: 'test.php', //仅为示例，并非真实的接口地址
  data: {
     x: '' ,
     y: ''
  },
  header: {
      'content-type': 'application/json' // 默认值
  },
  success: function(res) {
    console.log(res.data)
  }
})
```

```javascript
// utils/requestMethod.js
let serverPath = 'http://www.abc.com/api/';
export function post(url,body) {
    return new Promise((resolve,reject) => {
        wx.request({
              url: serverPath + url,    // 拼接完整的url
              data: body,
              method:'POST',
              header: {
                  'content-type': 'application/json'
              },
              success(res) {
                resolve(res.data)  // 把返回的数据传出去
              },
              fail(ret) {
                reject(ret)   // 把错误信息传出去
              }
            })
    })
}


import { post } from '/src/utils/requestMethod.js'
// 需要注意的是，这行代码必须要在async修饰的函数里面才能正确调用
let res = await post('member/login',{ name: myname });
async res()
```

## 参考

* [美团小程序框架mpvue入门教程](https://github.com/noahlam/articles/blob/master/%E7%BE%8E%E5%9B%A2%E5%B0%8F%E7%A8%8B%E5%BA%8F%E6%A1%86%E6%9E%B6mpvue%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B.md)








