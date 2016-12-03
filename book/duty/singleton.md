### 单例模式(Singleton)

单例模式是非常常用的设计模式，核心是一个类有且只有一个实例。单例模式分为饿汉式和懒汉式

#### 饿汉式

```java
package com.design.singleton;

public class Singleton {

    private static final Singleton instance = new Singleton();

    private Singleton() {}

    public static Singleton getInstance() {
        return instance;
    }
}
```

#### 懒汉式

```java
package com.design.singleton;

public class Singleton {

    private static Singleton instance = null;

    private Singleton() {}

    public static Singleton getInstance()
    {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

