### JavaScript基础--异步和单线程

#### 什么是异步

```javascript
  // 异步
  console.log(100);
  setTimeout(function(){
    console.log(200);
  },1000)
  console.log(300);
  // 执行顺序 分别打印 100，300，200
```

```javascript
  // 同步
  console.log(100);
  alert(200); // 会等待，点击之后再打印 300
  console.log(300);
```

#### 前端异步的使用场景

> 在可能需要等待的地方,不能因为等待阻塞程序运行，所以，所有 `需要等待的情况` 都需要用到异步

-   定时任务:`setTimeout`,`setInverval`
-   网络请求:`ajax` 请求,动态`<img>`加载
-   事件绑定



