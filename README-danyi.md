### 单一职责原则
+ 单一职责原则（Single Responsibility Principle简称为SRP）：应该有且仅有一个原因引起类的变更；对于单一职责原则，建议是接口一定要做到单一职责，类的设计尽量做到只有一个原因引起改变；只要做过项目，肯定要接触到用户、机构、角色管理这些模块，基本上使用的都是RBAC模型（Role-Based Access Control基于角色的访问控制，通过分配和取消角色来完成用户权限的授予和取消，使动作主体（用户）和资源的行为（权限）分离，确实是一个很好的解决办法；
#### 项目说明
+ 需要用户管理，修改用户的信息，增加机构（一个人属于多个机构），增加角色等，用户有这么多的信息和行为要维护，设计出合理的架构；
##### 错误的例子
+ 把这些写到一个接口中，都是用户管理类中的元素；

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-1.jpg)

##### 错误的分析
+ 因为用户的属性和用户的行为没有分开，这是一个严重的错误，这个接口确实设计的一团糟，应该把用户的信息抽取成一个BO（Business Objecrt，业务对象），把行为抽取成一个Biz（Business Logic，业务逻辑）；
##### 按照分析的改进
+ 重新拆封成两个接口，IUserBO负责用户的属性，也就是IUserBO的职责就是收集和反馈用户的属性信息，IUserBiz负责用户的行为，完成用户信息的维护和变更；

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-2.jpg)

+ 这样在使用时要获得用户信息，就当是IUserBO实现类，要是希望维护用户的信息，就把它当作IUserBiz的实现类；如下面代码使用：

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-3.jpg)

##### 最终的设计
+ 在实际的使用中，我们更倾向于使用两个不同的类或接口，一个是IUserBO，一个是IUserBiz；使用单一原则思想；

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-4.jpg)

### 绝杀技，打破你的传统思维
#### 项目说明
+ 电话通话的时候有4个过程发生：拨号、通话、回应、挂机，设计出合理的架构；
##### 一般的设计

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-5.jpg)

![image](https://github.com/ningbaoqi/DesignModeAndFramework/blob/master/gif/pic-6.jpg)
