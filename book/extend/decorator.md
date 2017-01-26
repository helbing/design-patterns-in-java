### 装饰器模式（Decorator）

装饰器模式是一种用于代替继承的模式，无需通过继承增加子类就能拓展对象的新功能。使用对象的关联关系来代替继承，避免类型体系过度膨胀。

#### 例子

#### 鸟类接口

```java
package com.design.decorator;

public interface IBird {

    public void can();
}
```

#### 鸟实现

```java
package com.design.decorator;

public class Bird implements IBird {

    @Override
    public void can() {
        System.out.println("可以移动");
    }
}
```

#### 装饰器类

```java
package com.design.decorator;

public class Decorator implements IBird {

    protected IBird bird = null;

    public Decorator(Bird bird) {

        super();
        this.bird = bird;
    }

    @Override
    public void can() {
        bird.can();
    }
}
```

#### 鸭子类

```java
package com.design.decorator;

public class Duck extends Decorator {

    public Duck(Bird bird) {
        super(bird);
    }

    public void swin() {
        System.out.println("可以游");
    }

    @Override
    public void can() {
        super.can();
        this.swin();
    }
}
```

#### Main

```java
package com.design.decorator;

public class Main {

    public static void main(String[] args) {

        Bird bird = new Bird();
        bird.can();

        System.out.println("-------");

        Duck duck = new Duck(bird);
        duck.can();
    }
}
/**
 * 可以移动
 * -------
 * 可以移动
 * 可以游
 */
```

