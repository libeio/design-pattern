
## 单例模式 Singleton
- 没什么好说明的，最常用的设计模式。如果你
    + 想确保任何情况下都绝对只有一个实例；
    + 想在程序上(进程里)表现出"只存在一个实例"
  那么就可以使用它。
- 单例模式分为很多种，比如懒汉、饿汉等等。只接触过懒汉，所以这里只对它进行记录。

## 懒汉单例
- 是非线程安全的；更适用于非线程安全的只读；非线程写时注意资源的同步；
- 简单程序示例如下:
  ```c++
    class Singleton {
        static Singleton* instance;
        Singleton() {}
        ~Singleton() {}
    public:
        static Singleton* getInstance() {
            if (instance == nullptr) {
                instance = new Singleton();
            }
            return instance;
        }
        static void destroyInstance() {
            if (instance) delete instance;
        }
    };
  ```
  实现上要注意两点:
    + Singleton 类定义了 static 成员 instance, 并将其初始化为 Singleton 类的实例，这
      样就保证了进程中只存在唯一实例；
    + Singleton 类的构造函数是**非public**的，这是为了禁止从 Singleton 类外部调用构造
      函数。
- 在上述示例程序中，成员变量 instance 和类的构造函数都是私有的，不过如果你想将单例类
  定义为一个基类或模板类以作派生，也可以将这两部分定义为 protected 化。不过无论如何，
  都不应该 public 化。

## 单例双检
- [单例模式的双重检测](https://www.cnblogs.com/tangZH/p/10031337.html)
- 测试程序: NoCheck.cpp DoubleCheck.cpp
- 执行 NoCheck.cpp 程序时，多线程下可能会打印不止一个 `Construct SingleTon` 。
  执行 DoubleCheck.cpp 程序时，因为进行了双检，所以多线程下只打印了一次 `Construct SingleTon` 。
  
## 相关的设计模式
- 以下模式中，多数情况下只会生成一个实例:
    + AbstractFactory 模式
    + Builder 模式
    + Facade 模式
    + Prototype 模式
