
## 类的两种层次结构
- 类的功能层次结构
    + 当希望增加新功能时。
    + 假设现在有一个类 Something ，当我们想在 Something 中增加新功能时(增加一个具体
      方法)，会编写一个 Something 类的子类(派生类)，如 SomethingGood 类，这样就构成
      了一个类层次结构。
      ```shell
        Something
            |-- SomethingGood
      ```
      像上面这种层次结构称为"**类的功能层次结构**"，它具有以下特征:
        + 父类具有基本功能
        + 在子类中增加新的功能
- 类的实现层次结构
    + 当希望增加新的实现时。
    + 抽象类声明了一些抽象方法，定义了接口(API)，然后子类负责去实现这些抽象方法。父
      类的任务是通过声明抽象方法的方式定义接口(API)，而子类的任务是实现抽象方法。比
      如抽象类 AbstractClass 中定义了接口，子类 ConcreteClass 实现了抽象类中定义的
      方法，它们之间就构成了一个层次结构:
      ```shell
        AbstractClass
            |-- ConcreteClass
      ```
      像上面这种层次结构称为"**类的实现层次结构**"，它具有以下特征:
        + 父类通过声明抽象方法来定义接口
        + 子类通过实现具体方法来实现接口
- 类的层次结构的混杂与分离
    + 了解了类的两种层次结构后，那么当我们想要编写子类时，就需要先确认自己的意图: 是
      要增加功能呢？还是要增加实现呢？
    + 当类的实现只有一层时，功能层次结构与实现层次结构混杂在一个层次结构中。这样很容
      易使类的层次结构变得复杂。
    + 因此，我们需要将"类的功能层次结构"与"类的实现层次结构"分离为两个独立的类层次结
      构。当然，如果只是简单地将它们分开，两者之间必然会缺少联系。所以我们还需要在它
      们之间搭建一座桥梁。这就要用到桥接(Bridge)模式。

## 说明
- 设计模式的"桥接"不是"桥接"之后，两端可以平等的交流数据，而是架好一座从活动端(上层)
  到不动端(底层)的桥梁，这样活动端就可以访问不动端。
- 一般来说，类的实现层次结构是从整体的功能实现作把控，而类的功能层次结构在整体功能实
  现基础上进行具体的修缮。所以通常将类的功能层次视为活动端，将类的实现作为不动端。
- 用户对程序的调用及维护工作量也主要体现在上层主动端，即类的功能层次结构。

## realize 实现
- 先进行实现层的书写，为了便于后续整体的替换采用多态实现方式。相关类有 DisplayImpl 和
  StringDisplayImpl 。
- 之后进行功能层的修缮，涉及到的类有 Display 和 CountDisplay 。 Display 以成员内聚的方
  式完成了与实现层的桥接，因为功能层只是局部的修补，所以使用一般继承即可完成任务。
- 示例程序: realize.cpp

## 其他
- 上述阐述了功能与实现的桥接的思想过程，实际上桥接的思想也被用于功能与数据之间，这时
  功能层作为活动端，数据端作为被动端。
- 示例程序: realize2.cpp

## 相关的设计模式
- Template Method 模式
    + 在 Template Method 模式中使用了"类的实现层次结构"。父类调用抽象方法，而子类实现
      抽象方法。
- AbstractFactory 模式
    + 为了能够根据需求设计出良好的"具体实现层"，有时我们会使用 AbstractFactory 模式。
- Adapter 模式
    + 使用 Bridge 模式可以达到类的功能层次结构与类的实现层次结构分离的目的，并在此基础
      上使这些层次结构结合起来。
    + 而使用 Adapter 模式则可以结合那些功能上相似但是接口(API)不同的类。即 Apapter 模
      式的接口统一于抽象层，而桥接模式的接口统一于功能层。