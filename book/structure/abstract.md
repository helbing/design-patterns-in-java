### 抽象工厂模式(Abstract Factory)

抽象工厂模式其实是工厂方法模式的一种扩展，应用抽象工厂模式可以创建一系列的产品（产品族），而不是像工厂方法模式中的只能创建一种产品。

比如富士康有两条产品线，一个是手机，一个是平板电脑，同时有苹果和小米这两个牌子的产品需要生产，所以总共有四条产品线。

#### 手机接口

```java
package com.design.abstracts;

public interface Phone {

    public void production();
}
```

#### 平板接口

```java
package com.design.abstracts;

public interface Pad {

    public void production();
}
```

#### iphone生产线

```java
package com.design.abstracts;

public class Iphone implements Phone {

    public void production()
    {
        System.out.println("生产苹果手机");
    }
}
```

#### ipad生产线

```java
package com.design.abstracts;

public class Ipad implements Pad {

    public void production()
    {
        System.out.println("生产苹果平板");
    }
}
```

#### mphone生产线

```java
package com.design.abstracts;

public class Mphone implements Phone {

    public void production()
    {
        System.out.println("生产小米手机");
    }
}
```

#### mpad生产线

```java
package com.design.abstracts;

public class Mpad implements Pad {

    public void production()
    {
        System.out.println("生产小米平板");
    }
}
```

#### 工厂

```java
package com.design.abstracts;

public class Factory {

    private Iphone iphone = null;
    private Ipad ipad = null;
    private Mphone mphone = null;
    private Mpad mpad = null;

    public Factory() {
        this.iphone = new Iphone();
        this.ipad = new Ipad();
        this.mphone = new Mphone();
        this.mpad = new Mpad();
    }

    public void iphone() {
        this.iphone.production();
    }

    public void ipad() {
        this.ipad.production();
    }

    public void mphone() {
        this.mphone.production();
    }

    public void mpad() {
        this.mpad.production();
    }
}
```

#### Main

```java
package com.design.abstracts;

public class Main {

    public static void main(String[] args) {
        Factory factory = new Factory();
        factory.iphone();
        factory.ipad();
        factory.mphone();
        factory.mpad();
    }
}
/**
 * 生产苹果手机
 * 生产苹果平板
 * 生产小米手机
 * 生产小米平板
 */
```



