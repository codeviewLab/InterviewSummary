关于javascript
---
>javascript是一门单线程语言

javascript 事件循环
---
既然js是单线程，js代码也要一行一行顺序执行。如果一个任务耗时过长，那么后一个任务也必须等着。那么问题来了，假如我们想浏览新闻，但是新闻包含的超清图片加载很慢，难道我们的网页要一直卡着直到图片完全显示出来？因此聪明的程序员将任务分为两类：

- 同步任务
- 异步任务

当我们打开网站时，网页的渲染过程就是一大堆同步任务，比如页面骨架和页面元素的渲染。而像加载图片音乐之类占用资源大耗时久的任务，就是异步任务。如图：

![](http://orvwtnort.bkt.clouddn.com/201721343/1535095879792.png)


>1.同步和异步任务分别进入不同的执行"场所"，同步的进入主线程，异步的进入`Event Table`并注册函数。
2.当指定的事情完成时，`Event Table`会将这个函数移入`Event Queue`。
3.主线程内的任务执行完毕为空，会去`Event Queue`读取对应的函数，进入主线程执行。
4.上述过程会不断重复，也就是常说的`Event Loop`(事件循环)。

举例：
```
let data = [];
$.ajax({
    url:www.javascript.com,
    data:data,
    success:() => {
        console.log('发送成功!');
    }
})
console.log('代码执行结束');
```
上面是一段简易的ajax请求代码：

- `ajax`进入`Event Table`，注册回调函数`success`。
- 执行`console.log('代码执行结束')`。
- `ajax`事件完成，回调函数`success`进入`Event Queue`。
- 主线程从`Event Queue`读取回调函数`success`并执行。

精细粒度
---
除了广义的同步任务和异步任务，我们对任务有更精细的定义：

>- `macro-task`(宏任务)：包括整体代码`script`，`setTimeout`，`setInterval`
>- `micro-task`(微任务)：`Promise`，`process.nextTick`

举例：
```
console.log('script start');

setTimeout(function() {
  console.log('setTimeout');
}, 0);

Promise.resolve().then(function() {
  console.log('promise1');
}).then(function() {
  console.log('promise2');
});

console.log('script end');
```


>1.一开始`task`队列中只有`script`，则`script`中所有函数放入函数执行栈执行，代码按顺序执行。

>2.接着遇到了`setTimeout`,它的作用是0ms后将回调函数放入`task`队列中，也就是说这个函数将在下一个事件循环中执行（注意这时候`setTimeout`执行完毕就返回了）。

>3.接着遇到了`Promise`，按照前面所述`Promise`属于`microtask`，所以第一个.then()会放入`microtask`队列。

>4.当所有`script`代码执行完毕后，此时函数执行栈为空。开始检查`microtask`队列，此时队列不为空,执行`.then()`的回调函数输出`'promise1'`，由于`.then()`返回的依然是`promise`,所以第二个`.then()`会放入`microtask`队列继续执行,输出`'promise2'`。

>5.此时`microtask`队列为空了，进入下一个事件循环，检查`task`队列发现了`setTimeout`的回调函数，立即执行回调函数输出'setTimeout'，代码执行完毕。

参考文章
---
[这一次，彻底弄懂 JavaScript 执行机制](https://juejin.im/post/59e85eebf265da430d571f89)  
https://segmentfault.com/a/1190000010622146  
https://github.com/dwqs/blog/issues/61  
https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/  
https://github.com/aooy/blog/issues/5  
https://github.com/rhinel/blog-word/issues/4  
