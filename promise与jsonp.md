---
title: promise与jsonp
date: 2020-06-18 09:01:47
tags:
- web
- jsonp
- promise
categories: 
- 学习笔记
- javaScript
---

​			学习链接	: [知乎](https://zhuanlan.zhihu.com/p/42377418)  [阮一峰](https://es6.ruanyifeng.com/#docs/promise#Promise-%E7%9A%84%E5%90%AB%E4%B9%89)  [promise/A+规范](https://promisesaplus.com/)  [Bilibili尚硅谷学习promise学习教程](https://www.bilibili.com/video/BV1MJ41197Eu?p=2)

## 一 Promise/A+<sup>[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)</sup>

### 1. 何为promise:

promise是一种**解决方案**,用于处理异步编程中回调问题,比传统的回调函数更加合理易用.

这里的回调问题主要是**函数名不统一**和**[回调地狱](https://mp.weixin.qq.com/s?__biz=MzI4OTc3NDgzNQ==&mid=2247484700&idx=1&sn=0a840596519263dd8baa1e4a0f265151&chksm=ec2b4880db5cc196a314f2b00eee6a070f06bfe76c78520dd1dfb1c580fd2854b5bea1e52b92&mpshare=1&scene=23&srcid=05018Hm3bknNtywEJv1Yn5T2#rd)**问题,例如在使用第三方库的ajax时,调用传统的回调函数,需要知道函数参数的名称,有的是succ,有的可以是done等等.所以需要统一的风格来共用一套解决方案,所以有了promise来处理这个问题;回调地狱是由于多重函数作为参数层层嵌套,最后造成可读性很差、代码量巨大、可维护性差等问题.

promise在语法上是一个**对象**,构造函数

```js
new Promise( function(resolve, reject) {...} /* executor */  );
```

promise对象包含:
- 三种状态:
  -  pending(待定)
  -  fulfill(完成)
  -  rejected(失败)  
- 两个函数参数:
  - resolve
  - reject 

  其中调用过程如下:
    ![调用过程](https://mdn.mozillademos.org/files/8633/promises.png)
  

### 2.使用方法

```js
//创建一个promise
const myFirstPromise = new Promise((resolve, reject) => {
// ?做一些异步操作，最终会调用下面两者之一:
//
//   resolve(someValue); // fulfilled
// ?或
//   reject("failure reason"); // rejected
});

//让某个函数拥有promise功能
function myAsyncFunction(url) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url);
    xhr.onload = () => resolve(xhr.responseText);
    xhr.onerror = () => reject(xhr.statusText);
    xhr.send();
  });
};

```

```js
//例1:
function getUserId() {
    return new Promise(function(resolve) {
        //异步请求
        http.get(url, function(results) {
            resolve(results.id)
        })
    })
}

getUserId().then(function(id) {
    //一些处理
})

//例2:
function xxx(){
    return new Promise((resolve, reject)=>{
		doyouwork();
        cosnt res;
        cosnt err;
        setTimeout(()=>{
            if(success){
            resolve().call(undefined,res)
        	}else{
            reject().call(undefined,err)
        }
        })
    })
}

xxx().then(succ(res),fail(err))  ///调用
```

```js
//简单原型结构
function Promise(fn) {
    var value = null,
        callbacks = [];  //callbacks为数组，因为可能同时有很多个回调

    this.then = function (onFulfilled) {
        callbacks.push(onFulfilled);
    };

    function resolve(value) {
        callbacks.forEach(function (callback) {
            callback(value);
        });
    }
    
    fn(resolve);
}
```

- getUserId返回的Promise对象通过then注册它成功的回调函数 

- 从数据结构的角度就是promise调用自身的then方法,向callbacks队列push进去一个函数对象, 实现入队操作



### 3.成员方法:

![image-20200618132622539](https://i.loli.net/2020/06/18/tLHNSW6TqJz7Xdf.png)

​	

- [`Promise.all(iterable)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

  这个方法返回一个新的promise对象，该promise对象在iterable参数对象里所有的promise对象都成功的时候才会触发成功，一旦有任何一个iterable里面的promise对象失败则立即触发该promise对象的失败。这个新的promise对象在触发成功状态以后，会把一个包含iterable里所有promise返回值的数组作为成功回调的返回值，顺序跟iterable的顺序保持一致；如果这个新的promise对象触发了失败状态，它会把iterable里第一个触发失败的promise对象的错误信息作为它的失败错误信息。Promise.all方法常被用于处理多个promise对象的状态集合

  常见的应用场景有页面加载多个ajax数据回来以前，保持loading显示，或者加载失败后进行异步操作

- [`Promise.race(iterable)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/race)

  当iterable参数里的任意一个子promise被成功或失败后，父promise马上也会用子promise的成功返回值或失败详情作为参数调用父promise绑定的相应句柄，并返回该promise对象

  如Promise.race([p1, p2, p3]), 应用场景有超时机制

- [`Promise.reject(reason)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject)

  返回一个状态为失败的Promise对象，并将给定的失败信息传递给对应的处理方法

- [`Promise.resolve(value)`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve)

  返回一个状态由给定value决定的Promise对象。如果该值是thenable(即，带有then方法的对象)，返回的Promise对象的最终状态由then方法执行决定；否则的话(该value为空，基本类型或者不带then方法的对象),返回的Promise对象状态为fulfilled，并且将该value传递给对应的then方法。通常而言，如果你不知道一个值是否是Promise对象，使用Promise.resolve(value) 来返回一个Promise对象,这样就能将该value以Promise对象形式使用。
  
- Promise.prototype.then(onFulfilled[, onRejected])

  当 Promise 变成接受状态（fulfilled）时调用的[`函数`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Function)。该函数有一个参数，即接受的最终结果（the fulfillment  value）。如果该参数不是函数，则会在内部被替换为 `(x) => x`，即原样返回 promise 最终结果的函数
  当 Promise 变成拒绝状态（rejected）时调用的[`函数`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Function)。该函数有一个参数，即拒绝的原因（`rejection reason`）。 如果该参数不是函数，则会在内部被替换为一个 "Thrower" 函数 (it throws an error it received as argument)
  当一个 [`Promise`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 完成（fulfilled）或者失败（rejected）时，返回函数将被异步调用（由当前的线程循环来调度完成）

### 4.来日补充



## 二 JSONP

### 1.JSON

​	javascript是一种是一种具有函数优先的轻量级，解释型或即时编译型的编程语言脚本语言

​	json是一种数据格式化语言 

​	jsonp是一种JSON扩展，是一种JSON的使用格式

​	json是以键值对的形式进行对数据交换的支持，语法支持对象、数组、字符串、数值、null、Boolean，相比javacript少了symbol和undefined。

​	主要的用处在于交换数据，比如动态网页想要数据的写数据，发送请求后服务器把数据转换为json格式，客户端接受json并解析其中的文本内容以应用到网页上。

​	JSON[官网](https://www.json.org/json-zh.html)

### 2.JSONP

​	*JSONP or "JSON with padding" is a JSON extension wherein a prefix is specified as an input argument of the call itself.*

​	jsonp模式可以破除跨域同源限制进行第三方数据访问, 此外用其他标签通过添加[CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)协议的请求头也可以实行跨域资源访问,只不过需要和后端协调

```
//jsonp格式
	parseRespone{		//--->这就是padding
​	"key1" : "String"

​	"key2" : 233 		//--->"键":值

}					//--->这也是padding
```



​	JSONP使用json的使用模式：

  1. 使用js标签
     	由于js标签没有[跨域同源](https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy)的限制(即同协议、同端口、同主机)，使用\<script>标签，src指向需要请求的网址如：

     ```js
     <script src= "https://cn.bing.com/?scope=web/" ></script>
     ```

     ​	值的注意的是，**jsonp只能用get方法，因为jsonp借助的是js动态标签，而动态标签只能用get**

		2. 约定回调
      响应方获取请求方提供的回调函数名，做相应的处理后返回JSON数据的封装，形如上面的中的jsonp格式

		3. 调用回调
     
     请求方获取json封装的服务器响应数据，并解析获取其中内容，调用回调函数后，加载到网页上

至此jsonp完成,总结两点:

- JSONP是通过 script 标签加载数据的方式去获取数据当做 JS 代码来执行

- 提前在页面上声明一个函数，函数名通过接口传参的方式传给后台，后台解析到函数名后在原始数据上「包裹」这个函数名，发送给前端。换句话说，JSONP 需要对应接口的后端的配合才能实现。

完整示例：

```js
//jquery的ajax封装
$.ajax({
	url:"www.exmaple.com/fuck",
	dataType: "jsonp",
	success: fucntion(response){
		doyouwork()
	},
	fail: function(err){console.log(err)}
})
```

​	