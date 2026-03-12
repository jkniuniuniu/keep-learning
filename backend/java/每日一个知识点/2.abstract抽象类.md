### 1. 定义抽象类（阿里开发手册抽象类的命名：抽象类命名要使用 Abstract 或 Base 开头）

```java
abstract class AbstractPlayer {
}
```

### 2. 抽象类的特征
- 抽象类是不能实例化的（new），但是可以继承（extends）
- 如果一个类定义了一个或多个抽象方法，那么这个类必须是抽象类。
- 抽象类中既可以定义抽象方法，也可以定义普通方法，就像下面这样：
```java
public abstract class AbstractPlayer {
    abstract void play();
    
    public void sleep() {
        System.out.println("运动员也要休息而不是挑战极限");
    }
}
```
- 抽象类派生的子类必须实现父类中定义的抽象方法。比如说，抽象类 AbstractPlayer 中定义了 play() 方法，子类 BasketballPlayer 中就必须实现。
```java
public class BasketballPlayer extends AbstractPlayer {
    @Override
    void play() {
        System.out.println("我是张伯伦，篮球场上得过 100 分");
    }
}
```

### 3. 抽象类的应用场景 `(service接口和实现)`
- 当我们需要在抽象类中定义好 API，然后在子类中扩展实现的时候就可以使用抽象类。比如说，AbstractPlayer 抽象类中定义了一个抽象方法 play()，表明所有运动员都可以从事某项运动，但需要对应子类去扩展实现，表明篮球运动员打篮球，足球运动员踢足球。
```java
abstract class AbstractPlayer {
    abstract void play();
}
```
BasketballPlayer 继承了 AbstractPlayer 类，扩展实现了自己的 play() 方法。
```java
public class BasketballPlayer extends AbstractPlayer {
    @Override
    void play() {
        System.out.println("我是张伯伦，我篮球场上得过 100 分，");
    }
}
```
FootballPlayer 继承了 AbstractPlayer 类，扩展实现了自己的 play() 方法。
```java
public class FootballPlayer extends AbstractPlayer {
    @Override
    void play() {
        System.out.println("我是C罗，我能接住任意高度的头球");
    }
}
```

### 4. 抽象类总结
1. 抽象类不能被实例化。
2. 抽象类应该至少有一个抽象方法，否则它没有任何意义。
3. 抽象类中的抽象方法没有方法体。
4. 抽象类的子类必须给出父类中的抽象方法的具体实现，除非该子类也是抽象类。

### 5. 个人理解
- 迷惑点：抽象类只是定义了抽象方法，抽象方法最后还是要靠开发者去实现它的具体逻辑，那我为什么还要多加这一层抽象类呢？？我直接去写代码逻辑不就好了么？

    `请求 -> 抽象类方法 -> 抽象类方法实现（具体逻辑）`

- 解惑：
1. 抽象类是可以省略的，一些小的项目用抽象类反而是累赘。
2. 抽象类是从设计角度出发的，比如我框架想要所有页面的查询都调用search，所有的更新都调用update，那我就需要定义一个抽象类，里面提供search 和 update抽象方法，每个页面去自己实现search和update的具体业务。
3. 再深入一些，比如我项目要求每次执行update前必须执行排他处理，如果让开发者去实现的话，开发者就自己想着写排他处理，有时候写着写着就给忘了，如果我这时候抽象类中定义好，update前必须还要要排他处理，那我开发者写实现逻辑的时候如果忘记了写排他的实现，代码就直接报错了，能有一定的规范性和检查性。
