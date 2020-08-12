---
title: "005 Design_principles"
date: 2020-07-22T22:18:33+08:00
draft: false
tags: [principles]
---

## 面向对象的设计原则

设计原则是2002年 罗伯特·塞西尔·马丁 (Robert Cecil Martin)俗称“鲍伯叔叔” [敏捷软件开发：原则、模式与实践/软件工程实践丛书](https://item.jd.com/12468135.html)书中提到可重用的五大设计原则 - “SOLID”（英文首字母缩略字）:

- Single Responsibility Principle - 单一职责
- Open / Closed Principle - 开闭原则
- Liskov Substitution Principle - 里氏替换原则
- Interface Segregation Principle - 接口隔离原则
- Dependency Inversion Principle - 依赖倒置原则


### 一、单一职责原则
该原则提出对象不应该承担太多职责，如果一个对象承担了太多的职责，至少存在以下两个缺点：
- 一个职责的变化可能会削弱或者抑制这个类实现其他职责的能力；
- 当客户端需要该对象的某一个职责时，不得不将其他不需要的职责全都包含进来，从而造成冗余代码或代码的浪费。

单一职责的核心就是控制类的粒度大小、将对象解耦、提高其内聚性

#### 1、单一职责的优点
- 降低类的复杂度。一个类只负责一项职责，其逻辑肯定要比负责多项职责简单得多。
- 提高类的可读性。复杂性降低，自然其可读性会提高。
- 提高系统的可维护性。可读性提高，那自然更容易维护了。
- 变更引起的风险降低。变更是必然的，如果单一职责原则遵守得好，当修改一个功能时，可以显著降低对其他功能的影响。

#### 2、单一职责原则的实现方法
单一职责原则是最简单但又最难运用的原则，需要设计人员发现类的不同职责并将其分离，再封装到不同的类或模块中。而发现类的多重职责需要设计人员具有较强的分析设计能力和相关重构经验。

### 二、开闭原则
开闭原则（OCP）即对修改关闭，扩展开放。代码模块应该在修改代码的的情况下，进行代码的扩展。一般需要通过接口和抽象实现该效果。
开闭原则的含义是当应用的需求改变时，在不修改软件实体代码的源代码或二进制代码的前提下，可以扩展模块功能以满足需求。

#### 1、开闭原则的作用

开闭原则是面向对象设计的终极目标，它使软件设计有一定的适应性和灵活性。其作用如下：
- 对软件测试的影响

    遵守原则的情况下，测试可以只对扩展代码进行测试

- 可以提高代码的可复用性

    遵守原则，粒度越小，被复用的可能性越大

- 可以提高软件的可维护性

    遵守原则，其稳定性高，持续性强，从而易于维护和扩展

#### 2、开闭原则的实现方法
可以通过“抽象约束、封装变化”来实现开闭原则，即通过接口或者抽象类为软件实体定义一个相对稳定的抽象层，而将相同的可变因素封装在相同的具体实现类中

因为抽象灵活性好，适应性广，只要抽象的合理，可以基本保持软件架构的稳定。而软件中易变的细节可以从抽象派生来的实现类来进行扩展，当软件需要发生变化时，只需要根据需求重新派生一个实现类来扩展就可以了。

下面以 汽车和4S店为例介绍开闭原则的应用。
分析：4s店销售各种型号品牌的汽车，汽车的价格、型号不一样。这些汽车有共同的属性，抽象出一个汽车分类。4s店进一个新型号的汽车，实现这个抽象类就可以，不影响其他型号。如下图所示
![avatar](open-close.png)

### 三、里氏替换原则
里氏替换原则主要阐述了有关继承的一些原则，也就是什么时候应该使用继承，什么时候不应该使用继承，以及其中蕴含的原理。里氏替换原是继承复用的基础，它反映了基类与子类之间的关系，是对开闭原则的补充，是对实现抽象化的具体步骤的规范。

#### 1、里氏替换原则的作用

- 里氏替换原则是实现开闭原则的重要方式之一
- 它克服了继承中重写父类造成的可复用性变差的缺点
- 它是动作正确性的保证。即类的扩展不会给已有的系统引入新的错误，降低了代码出错的可能性。

#### 2、里氏替换原则的实现方法
里氏替换原则通俗来讲就是：子类可以扩展父类的功能，但不能改变父类原有的功能。也就是说：子类继承父类时，除添加新的方法完成新增功能外，尽量不要重写父类的方法。

如果通过重写父类的方法来完成新的功能，这样写起来虽然简单，但是整个继承体系的可复用性会比较差，特别是运用多态比较频繁时，程序运行出错的概率会非常大。

如果程序违背了里氏替换原则，则继承类的对象在基类出现的地方会出现运行错误。这时其修正方法是：取消原来的继承关系，重新设计它们之间的关系。

### 四、接口隔离原则
接口隔离原则（Interface Segregation Principle，ISP）要求程序员尽量将臃肿庞大的接口拆分成更小的和更具体的接口，让接口中只包含客户感兴趣的方法。
接口隔离原则和单一职责都是为了提高类的内聚性、降低它们之间的耦合性，体现了封装的思想，但两者是不同的：
- 单一职责原则注重的是职责，而接口隔离原则注重的是对接口依赖的隔离。
- 单一职责原则主要是约束类，它针对的是程序中的实现和细节；接口隔离原则主要约束接口，主要针对抽象和程序整体框架的构建。

#### 1、接口隔离原则的优点

接口隔离原则是为了约束接口、降低类对接口的依赖性，遵循接口隔离原则有以下 5 个优点。
1、将臃肿庞大的接口分解为多个粒度小的接口，可以预防外来变更的扩散，提高系统的灵活性和可维护性。
2、接口隔离提高了系统的内聚性，减少了对外交互，降低了系统的耦合性。
3、如果接口的粒度大小定义合理，能够保证系统的稳定性；但是，如果定义过小，则会造成接口数量过多，使设计复杂化；如果定义太大，灵活性降低，无法提供定制服务，给整体项目带来无法预料的风险。
4、使用多个专门的接口还能够体现对象的层次，因为可以通过接口的继承，实现对总接口的定义。
5、能减少项目工程中的代码冗余。过大的大接口里面通常放置许多不用的方法，当实现这个接口的时候，被迫设计冗余的代码。

#### 2、接口隔离原则的实现方法
在具体应用接口隔离原则时，应该根据以下几个规则来衡量。
1、接口尽量小，但是要有限度。一个接口只服务于一个子模块或业务逻辑。
2、为依赖接口的类定制服务。只提供调用者需要的方法，屏蔽不需要的方法。
3、了解环境，拒绝盲从。每个项目或产品都有选定的环境因素，环境不同，接口拆分的标准就不同深入了解业务逻辑。
4、提高内聚，减少对外交互。使接口用最少的方法去完成最多的事情。





### 五、依赖倒置原则
依赖倒置原则的原始定义为：高层模块不应该依赖低层模块，两者都应该依赖其抽象；抽象不应该依赖细节，细节应该依赖抽象。其核心思想是：要面向接口编程，不要面向实现编程。

依赖倒置原则是实现开闭原则的重要途径之一，它降低了客户与实现模块之间的耦合。

由于在软件设计中，细节具有多变性，而抽象层则相对稳定，因此以抽象为基础搭建起来的架构要比以细节为基础搭建起来的架构要稳定得多。这里的抽象指的是接口或者抽象类，而细节是指具体的实现类。

使用接口或者抽象类的目的是制定好规范和契约，而不去涉及任何具体的操作，把展现细节的任务交给它们的实现类去完成。

#### 1、依赖、倒置原则的作用
- 依赖倒置原则可以降低类间的耦合性。
- 依赖倒置原则可以提高系统的稳定性。
- 依赖倒置原则可以减少并行开发引起的风险。
- 依赖倒置原则可以提高代码的可读性和可维护性。

#### 2、依赖倒置原则的实现方法
依赖倒置原则的目的是通过要面向接口的编程来降低类间的耦合性，所以我们在实际编程中只要遵循以下4点，就能在项目中满足这个规则。

- 每个类尽量提供接口或抽象类，或者两者都具备。
- 变量的声明类型尽量是接口或者是抽象类。
- 任何类都不应该从具体类派生。
- 使用继承时尽量遵循里氏替换原则。

#### 3、依赖倒置原则的实现方法

依赖倒置原则的目的是通过要面向接口的编程来降低类间的耦合性，所以我们在实际编程中只要遵循以下4点，就能在项目中满足这个规则。
- 每个类尽量提供接口或抽象类，或者两者都具备。
- 变量的声明类型尽量是接口或者是抽象类。
- 任何类都不应该从具体类派生。
- 使用继承时尽量遵循里氏替换原则。



### ChangeLog
- 2020年7月22日 完成单一职责和开闭原则


### 参考资料
http://c.biancheng.net/view/1324.html