### 策略模式(Strategy)

策略模式属于对象的行为模式。其用意是针对一组算法，将每一个算法封装到具有共同接口的独立的类中，从而使得它们可以相互替换。策略模式使得算法可以在不影响到客户端的情况下发生变化。

#### 例子

以旅游出行为例子讲解策略模式，在旅行中我们是可以根据自身的情况来选择交通工具的

#### 交通工具类

```java
package com.design.stragety;

public interface Traffic {

    public String vehicle();
}
```

#### 大巴类

```java
package com.design.stragety;

public class Bus implements Traffic {

    public String vehicle() {
        return "坐大巴";
    }
}
```

#### 飞机类

```java
package com.design.stragety;

public class Plane implements Traffic {

    public String vehicle() {
        return "坐飞机";
    }
}
```

### 旅行类

```java
package com.design.stragety;

public class Travel {

    private String destination = "";

    private Traffic traffic = null;

    public Travel(String destination)
    {
        this.destination = destination;
    }

    public void setTraffic(Traffic traffic) {
        this.traffic = traffic;
    }

    public void go() {
        System.out.println(this.traffic.vehicle() + "到" + this.destination + "旅行");
    }
}
```

#### Main

```java
package com.design.stragety;

public class Main {

    public static void main(String[] args) {

        Travel travel = new Travel("海南岛");
        // 选择交通工具
        travel.setTraffic(new Plane());
        travel.go();
    }
}

/**
 * 结果为
 * 坐飞机到海南岛旅行
 */
```



