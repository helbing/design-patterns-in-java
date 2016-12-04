### 工厂方法模式(Factory Method)

#### 例子

假设我们需要开发一个数据库驱动类，既要能支持Mysql，Oracle连接，同时支持拓展

#### DB接口

```java
package com.design.factory;

interface DB {
    public void connect();
}
```

#### Mysql类

```java
package com.design.factory;

public class Mysql implements DB {

    public void connect() {
        System.out.println("连接到Mysql");
    }
}
```

#### Oracle类

```java
package com.design.factory;

public class Oracle implements DB {

    public void connect() {
        System.out.println("连接到Oracle");
    }
}
```

#### Factory类

```java
package com.design.factory;

public class Factory {

    public DB getDB(String className) {
        try {
          	// 根据类名获取到DB实例
            return (DB)Class.forName(className).newInstance();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
        return null;
    }
}
```

#### Main

```java
package com.design.factory;

public class Main {

    public static void main(String[] args) {
        Factory factory = new Factory();
        DB db = factory.getDB("com.design.factory.Oracle");
        db.connect();
    }
}
```

在实际开发中可以将"com.design.factory.Oracle"写入到配置文件中，这样每次更改数据库连接只需要修改配置文件而不需要重启服务。





