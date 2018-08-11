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

##### 按照分析的改进
+ 将美女分成气质型美女和美丽型美女； 

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-46.jpg)

##### 两种类型的美女定义

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-47.jpg)

##### 最标准的美女

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-48.jpg)

+ 通过这样的重构，不管以后是要气质美女还是外形美女，都可以保持接口的稳定，当然，有人会说，以后可能审美观点发生变化了，那接口还是需要修改呀，确实是的，但是设计是有限度的，不能无限的考虑未来的变更情况，否则就会陷入设计的泥潭中而无法自拔；以上将一个臃肿的接口变更为两个独立的接口所依赖的原则就是接口隔离原则，让星探AbstractSearcher依赖两个专门的接口比依赖一个综合的接口要灵活，接口是我们设计时对外提供的契约，通过分散定义多个接口，可以预防未来变更的扩散，提高系统的灵活性和可维护性；

|接口隔离原则是对接口进行规范约束，其包含以下4层含义|
|------|
|接口要尽量小:这是接口隔离原则的核心定义，不出现臃肿的接口，但是小是有限度的，首先就是不能违反单一职责原则；所以：根据接口隔离原则拆分接口时，首先必须满足单一职责原则；|
|接口要高内聚:高内聚就是提高接口、类、模块的处理能力，减少对外的交互；具体的接口隔离原则就是，要求在接口中尽量少公布public方法，接口是对外的承诺，承诺越少对系统的开发越有利，变更的风险也就越少，同时也有利于降低成本；|
|定制服务: 一个系统或系统内的模块之间必然会有耦合，有耦合就要有互相访问的接口（并不一定就是Java中定义的interface，也可能是一个类或单纯的数据交换），我们设计时就需要为各个访问者（即客户端）定制服务，什么是定制服务？定制服务就是单独为一个个体提供优良的服务，我们在做系统设计时也需要考虑到对系统之间或模块之间的接口采用定制服务，采用定制服务就必然有一个要求，只提供访问者需要的方法；|
|接口设计是有限度的:接口的设计粒度越小，系统越灵活，这是不争的事实，但是，灵活的同时带来了结构的复杂化，开发难度增加，可维护性降低，这不是一个项目或产品所期望看到的，所以接口设计一定要注意适度，这个度如何来判断呢？根据经验和常识判断，没有一个固化或可测量的标准；|
