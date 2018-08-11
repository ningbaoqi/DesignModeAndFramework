### 接口隔离原则

|接口的分类|
|------|
|实现接口，在Java中声明一个类，然后使用new关键字产生一个实例，它是对一个类型的事物的描述，这是一种接口，比如你定义Person这个类，然后使用`Person person = new Person()`产生了一个实例，这个实例要遵从的标准就是Person这个类，Person类就是person的接口；|
|类接口，Java中经常使用的interface关键字定义的接口|

|隔离的定义|
|------|
|客户端不应该依赖它不需要的接口|
|类间的依赖关系应该建立在最小的接口上|

+ 客户需要什么接口就提供什么接口，把不需要的接口剔除掉，那就需要对接口进行细化，保证其纯洁性；总体来说，就是建立单一的接口，不要建立臃肿庞大的接口，也就是：接口尽量细化，同时接口中的方法尽量少，看到这里可能会有疑问？这不是和单一职责原则相同吗？不是的；接口隔离原则与单一职责原则的审视角度是不相同的，单一职责原则要求是类和接口职责单一，注重的是职责，这是业务逻辑上的划分，而接口隔离原则要求接口的方法尽量少，尽量使用多个专门的接口，专门的接口的含义是：提供给每个模块的都应该是单一接口，提供给几个模块就应该有几个接口，而不是建立一个庞大的臃肿的接口，容纳所有的客户端访问；

### 美女何其多、观点各不同
#### 项目说明
+ 星探和美女，设计合理的架构；
#### 错误的例子
+ 将气质优雅、美丽、身材妖娆全部写在同一个接口中； 

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-40.jpg)

##### 美女接口

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-41.jpg)

##### 美女实现类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-42.jpg)

##### 星探抽象类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-43.jpg)

##### 星探实现类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-44.jpg)

##### 场景类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-45.jpg)

##### 错误分析
+ 思考下IPettyGirl这个接口，这个接口是否做到了最优化设计？答案是否定的，还可以对接口进行优化；只有气质，其他方面一般，也属于美女；所以这个接口设计是有缺陷的，过于庞大了，容纳了一些可变的因素；