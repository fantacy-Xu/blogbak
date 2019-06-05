---
title: 设计者模式
date: 2019-06-03 16:54:45
tags: 设计者模式
---
# 设计者模式
---
   ## 设计模式
### 什么是设计模式
* 设计模式
     > 什么是设计模式
     > 设计模式（Design patern）是一套被反复使用、思想成熟、经过无数实战设计经验的总结。
     > 大白话：设计模式就是在特定场景解决特定的问题，如果某种办法都可以解决问题，我们就可以把这种通用的解决方法称之为模式。
     > 在代码中，其核心是代码的整体结构和解决问题的思路。
 ### 设计模式作用
 * 代码复用
 * 方便扩展
 * 增加可维护性
 * 其中设计模式最重要的一个原则是开闭原则，即对扩展 ，对修改关闭。
 * 单例模式概念：一个类只产生唯一的一个实例。因为在许多时候整个系统只需要拥有一个的全局对象，这样有利于我们协调系统整体的行为。
 * 作用：节省内存。
 * 应用场景：如商城系统中购车对象是单例的。
 * 示例1：创建单例对象
 ```
 function Person(){
    //核心：通过一个实例属性，来判断之前是否创建过//没有创建，则创建对象
        if( !Person.instance ){
        Person.instance = {};
        }//为真，说明有这个属性，则直接返回实例对象
        return Person.instance;
  }
    var p1 = Person();
    var p2 = Person();
    console.log(p1 === p2); // true 内存空间地址相同的。
 ````
 ### 工厂模式（构造函数模式）![645398560cc5076d5cca022c5dd88e46.png](en-resource://database/423:1)
> 生活中的工厂就是批量生产产品的地方。如一个服装工厂,可以生产衣服和裤子等。在代码中，工厂模式就是是由一个方法来决定到底要创建哪个类的实例。如：宝马工厂创建x1和x5品牌汽车
```
var factory = {};
factory.createProductA = function(){
    console.log('A');
}
factory.createProductB = function(){
    console.log('B');
}
factory.createProductC = function(){
    console.log('C');
}
factory.create = function(type){
    return new factory[type];
}//测试
factory.create('createProductA');
```
> 什么时候使用工厂模式，分为以下几种情景：
对象的构建较复杂生成大量不同对象的时候
策略模式每个问题都提前想好对应的解决方案（一种映射关系），而不是遇到问题再去手忙脚乱的想办法。
核心思想：提前想好策略.
代码：计算员工工资（工资由等级和底薪构成）//封装的策略算法
```
var strategies = {
    function (salary) {
         return salary * 4;
    },
    function (salary) {
         return salary * 3;
    },
    function (salary) {
        return salary * 2;
    }
 };//具体的计算方法
 var calculateBonus = function (level, salary) {
        return strategies[level](salary);
 };
 console.log(calculateBonus('S', 1000)); // 4000
 console.log(calculateBonus('A', 4000)); // 12000
```

使用策略模式重构代码，在实际开发中，可以消除程序中大片的条件分支语句。
### 适配器模式
通俗理解：比如苹果插座是三孔的,这时候我们想要充电,但是并没有三孔的插头,这时候我们就需要适配器转换一下,这样我们就可以充电的,这就是适配器模式解决问题的场景。
适配器模式侧重点在于转换接口,解决不兼容问题代码体现：在前端开发中，如果后台接口返回的是一个对象格式，但是我们的需求是需要数组格式，怎么办？（前后端开始撕逼了...）那么这种问题，我们前端完全可以按照适配器的思想去定义一个方法来实现对象到数组的转换。代码如下：
```
// 适配器模式// obj对象转换为数组
function objToArray(obj) {
    var arr = []; //新数组
for (var i in obj) {
    arr.push(obj[i]);
}
    return arr;
}
// 创建一个对象
var obj = {name: '大锤',age: 18,sex: '男'}// 适配器方式转换
console.log(objToArray(obj)); // [&quot;大锤&quot;, 18, &quot;男&quot;]
```
### 观察者模式
观察者模式也称之为发布订阅模式模式。它定义了一种一对多的关系，让多个观察者对象同时监听某一个发布者对象，这个发布者对象的状态发生改变时就会通知所有的观察者对象。如：多个人订阅微信公众号，微信公众号发布了文章，他们都可以收到。其中微信公众号就是发布者，其他人就是订阅者。代码:
```
//（发布者，微信公众号）被观察者
function ObServer(){//存储所有的订阅者（每一个订阅者是一个函数fn）
    this.funcs = [];
}
ObServer.prototype.subscribe = function(fn){
    this.funcs.push(fn);
}
ObServer.prototype.unsubscribe = function(fn){
    this.funcs = this.funcs.filter
    (function(item){
        if(item!==fn){
        return item;
         }
    })
}
ObServer.prototype.notify = function(msg){
    this.funcs.forEach(function(item){
    item(msg);
    });
}
var o = new ObServer();
var fn1 = function(msg){
    console.log('fn1收到通知了：'+msg);
}
var fn2 = function(msg){
    console.log('fn2收到通知了：'+msg);
}
o.subscribe(fn1);
o.subscribe(fn2);
o.notify('发布文章1');
o.unsubscribe(fn2);
console.log(o.funcs);
o.notify('发布文章2')
```
---
