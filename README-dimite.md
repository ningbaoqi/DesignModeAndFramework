### 迪米特法则
+ 迪米特法则（Law of Demeter，LoD）也称为最少知识原则（Least Knowledge Principle。LKP）：一个对象应该对其他对象有最少的了解，通俗的讲就是一个类应该对自己需要耦合或调用的类知道得最少，你（被耦合或调用的类）的内部是如何复杂的都和我没关系，那是你的事，我就知道你提供的这么多public方法，我就调用这么多，其他的我一概不关心；
### 我的知识你知道的越少越好
+ 迪米特法则对类的低耦合提出了明确的要求，其包含如下4层含义；
#### [一、只和朋友交流]()
+ 每个对象都必然会与其他的对象有耦合关系，两个对象之间的耦合就成为了朋友关系，这种关系的类型有很多，例如：组合、聚合、依赖等；
#### 项目说明
+ 模拟一个老师让体育委员确认一个全班女生到齐的情况，设计合理的架构；
##### 错误的例子

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-20.jpg)

##### 老师类的代码

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-21.jpg)

##### 体育委员GroupLeader类的代码

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-22.jpg)

##### 女生类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-23.jpg)

##### 场景类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-24.jpg)

##### 错误的分析
+ 首先确定Teacher类有几个朋友类，它仅有一个朋友类------GroupLeader，为什么Girl不是朋友类呢？Teacher也对它产生了依赖关系呀！朋友类的定义是这样的：出现在成员变量、方法的输入输出参数中的类称为成员朋友类，而出现在方法体内部的类不属于朋友类，而Girl这个类就是这种情况，因此不是朋友类；迪米特法则告诉我们一个类只和朋友类交流，但是我们定义的command方法却与Girl类有了交流；声明了一个`List<Girls>`动态数组，也就是与一个陌生类Girl有了交流，这样就破坏了Teacher的健壮性，方法是类的一个行为，类竟然不知道自己的行为与其他类产生依赖关系，这是不允许的，严重违反了迪米特法则；
