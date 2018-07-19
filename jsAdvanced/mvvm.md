## JS高级 —— MVVM

### 题目

#### 1. 说一下 jQuery 和使用框架的区别

-   jquery 实现todo list

    ```html
      <div>
          <input type="text" id="text">
          <button id="submit">提交</button>
      </div>
      <ul id="list"></ul>
    ```

    ```javascript
      var text = $('#text');
      var btn = $('#submit');
      var list = $('#list');
      btn.click(function(argument) {
          var title = text.val();
          if (!title) {
              return
          }
          var li = $('<li>' + title + '</li>');
          // 调用dom底层操作
          list.append(li);
          text.val('');
      })
    ```

-   vue 实现 todo list

    ```html
      <div id="app">
       <div>
           <input type="text" v-model="text">
           <button @click="add">提交</button>
       </div>
       <ul>
           <li v-for="item,index in list" :key="index">{{item}}</li>
       </ul>
     </div>
    ```

    ```javascript
      // 数据独立
      var data={
          text: '',
          list: []
      }
      // 初始化 vue 实例
      var app = new Vue({
          el: "#app",
          data: data,
          methods: {
              add() {
                  if (!this.text) {
                      return
                  }
                  // 只用改动数据，不用操作dom，以数据驱动视图
                  this.list.push(this.text);
                  this.text = '';
              }
          }
      })
    ```

-   两者的区别
    -   数据和视图的分离，解耦（开放封闭原则:对扩展开放，对修改封闭）
    -   以数据驱动视图，只关心数据变化，DOM 操作被封装

#### 2.说一下 MVVVM 的理解

-   MVVM
    -   Model 模型、数据
    -   View 视图、模板（视图和模型是分离的）
    -   ViewModel 连接Model和 View
-   MVVM 不算是一种创新
-   但是其中的 ViewModel 是一种创新
-   真正结合前端场景应用的创建
-   三要素
    -   1.如何监听到 data 的每个属性变化？
    -   2.Vue 的模板如何被解析，指令如何处理？
    -   3.Vue 的模板如何被渲染成 html ？以及渲染过程

#### 3.vue 如何实现响应

##### 响应式

    -   修改 data 属性之后，vue 立刻监听到
    -   data 属性被代理到 vm 上

##### Object.defineProperty

```javascript
   var key, vm = {};
   var data = { name: 'zhangsan', age: 18 };
   for (key in data) {
       (function(key) {
           Object.defineProperty(vm, i, {
               get: function() {
                   console.log('get', data[i])
                   return data[key];
               },
               set: function(newVal) {
                   console.log('set', newVal)
                   data[ikey] = newVal
               }
           })
       })(key)
   }
```

#### 4.vue 如何解析模板

##### 模板

-   模板本质是字符串
-   有逻辑，如 v-if v-for 等等
-   预备 html 格式很像，但有很大区别
-   最终还是要转换为 html 来显示
-   模板是什么
    -   模板最终必须转换成 JS 代码
    -   有逻辑（v-if v-for），必须用js才能实现（ JS 是图灵完备的语言）
    -   转换成 html 渲染页面，必须用 JS 才能实现
    -   因此，模板最终要转换成一个 JS 函数（ render 函数）

##### render函数

-   with 的用法

##### render函数 与 vdom

#### 5.vue 的整个实现流程

-   1.解析模板成 render 函数
-   2.响应式开始监听
-   3.首次渲染，显示页面，且绑定依赖
-   4.data属性变化，触发 rerender

#### MVVM

-   如何理解 MVVM
-   如何实现 MVVM
-   vue 源码
