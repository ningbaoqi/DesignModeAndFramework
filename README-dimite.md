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

##### 根据分析的优化

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-25.jpg)

##### 修改后的老师类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-26.jpg)

##### 修改后的体育委员类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-27.jpg)

##### 修改后的场景类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-28.jpg)

+ 对程序进行了简单的修改，把Teacher中对`List<Girl>`的初始化移动到了场景类中，同时在GroupLeader中增加了对Girl的注入，避开了Teacher类对陌生类Girl的访问，降低了系统间的耦合，提供了系统的健壮性；一个类只和朋友交流，不与陌生类交流，不要出现`getA().getB().getC().getD()`这种情况（在一种极端的情况下允许出现这种访问，即一个点号后面的返回类型都相同），类与类之间的关系是建立在类间的，而不是方法间的，因此一个方法尽量不引入一个类中不存在的对象，当然，JDK API提供的类除外；

#### [二、朋友间也是有距离的]()

##### 项目说明
+ 模拟安装软件，采用合理的架构；

##### 错误的例子

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-29.jpg)

##### 导向类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-30.jpg)

##### 安装软件类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-31.jpg)

##### 场景类

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-32.jpg)

+ Wizard类把太多的方法暴露给了InstallSoftware类，两者的朋友关系太密切了，耦合关系变得异常牢固，如果将Wizard类中的first方法返回值的类型由int改为boolean，就需要修改InstallSoftware类，从而把修改变更的风险扩散开了，因此，这样的耦合是极度不适合的，我们需要对设计进行重构；
