# micro-vm

> 通过学习自己封装一个框架, 来理解Vue内部实现双向数据绑定的原理

## 主流的双向数据绑定实现方式

1. 脏值检测 ==> Angular
2. 数据劫持 ==> Vue.js

**脏值检查:** angular 是通过脏值检测的方式比对数据是否有变更,来决定是否更新视图,最简单的方式就是通过 `setInterval()` 定时轮询检测数据变动,当然Google不会这么low,angular只有在指定的事件触发时进入脏值检测,大致如下：

- DOM事件,譬如用户输入文本,点击按钮等。( ng-click )
- XHR响应事件 ( $http )
- 浏览器Location变更事件 ( $location )
- Timer事件($timeout , $interval )
- 执行 $digest() 或 $apply()

**数据劫持:** vue.js 则是采用数据劫持结合发布者-订阅者模式(即观察者设计模式)的方式,通过`Object.defineProperty()`来劫持各个属性的`setter`,`getter`,在数据变动时发布消息给订阅者,触发相应的监听回调.

![](https://segmentfault.com/img/bVBQYu)



