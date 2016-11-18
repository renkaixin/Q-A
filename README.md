# Q-A
#### 1. Javascript 中如何精确判断一个变量类型？  
**答案:**
```javascript
function isNumber(a){
    return Object.prototype.toString.call(a).toLowerCase() === '[object number]'
}
```
#### 2. 考虑如下两种赋值方式，哪种更好？为什么？
```javascript
// A
(function(){
    var foo = 1;
    var bar = 1;
    var baz = 1;
})();
// B
(function(){
    var foo = bar = baz = 1;
})();
```
**答案:** A，因为B的链式赋值可能会在域内创造出2个全局变量bar和baz.

#### 3. Ecmascript2015中，yield 关键字的作用是什么？  
**答案:** yield 关键字在Generator中，中断当前执行流，返回结果，最终执行后面的代码流程
```javascript
function* foo() {
    let i = 0;
    while (i < 2) {
        yield i++;
    }
    console.log('hi');
}
var generator = foo();
generator.next(); // {value: 0, done: false}
generator.next(); // {value: 1, done: false}
generator.next(); // hi  {value: undefined, done: true}
```
koa框架的异步流程控制co就是用generator创建的，用同步的格式写异步代码

#### 4. 如何在Javascript代码中知道某个元素上的(CSS3动画/变换)的执行结束？  
**答案:**
```javascript
var element = document.getElementById("xxx");
// 可以加上对浏览器的兼容考察 -webkit -moz
element.addEventListener("transitionend", function() {}, false);
```

#### 5. 谈一谈前端的工具Grunt和Webpack，他们分别是什么？如果想在这个时代应用Ecmascript2015，需要什么样的工具？  
**答案:**
- Grunt是构建工具，可以将构建过程拆分成多个任务（Task），基础组件提供了clean, copy, uglify...，并且可以结合不同的TestRunner执行单元测试，构建打包的同时保证代码的稳健。
- Webpack是根据包依赖关系自动将多个资源整合成一个bundle.js。
- 如果是在NodeJs中，可以直接使用Ecmascript2015的绝大多数新功能。如果是在浏览器中，需要引入Bable.js这样的编译工具编译代码。


#### 6. 如何将程序流程移出同步队列？  
**答案:**
```javascript
console.log(1);
setTimeout(function () {
    console.log(3);
}, 0)
console.log(2);
```
