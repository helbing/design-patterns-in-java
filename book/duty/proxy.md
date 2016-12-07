### 代理模式(Proxy)

用生活中例子来解释代理模式就是，工厂，商店和顾客的关系，虽然顾客买东西可以到工厂和商店买东西，但是由于工厂地处偏僻而且顾客买的量少，工厂可能还不做你的生意。这时候商店的出现就能解决这些问题，由商店预估商品的未来销量，然后统一去工厂拿货，而且商店一般都会离住宅区很近。

在实际开发中我们可能需要对某一些代码进行记录日志和记录时间，我们可能会这么写

```java
System.out.println("执行前记录日志");
long start = System.currentTimeMillis();
try {
	// TODO
} catch (Exception e) {
	System.out.println(e.getMessage());
}
long end = System.currentTimeMillis();
System.out.println("执行时长" + (end - start) + "毫秒");
System.out.println("执行完记录日志");
```

如果太多代码需要进行记录日志和记录时间，这样写代码会过于冗余，这时候可以用代理模式，接下来用汽车的例子来解释代理模式

#### Move接口

```java
package com.design.proxy;

interface Move {

    public void move();
}
```

#### Car

```java
package com.design.proxy;

public class Car implements Move {

    public void move() {
        System.out.println("汽车行驶中");
    }
}
```

#### 记录时间

```java
package com.design.proxy;

public class Time implements Move {

    private Move move = null;

    public Time(Move move) {
        this.move = move;
    }

    public void move() {
        long start = System.currentTimeMillis();
        this.move.move();
        long end = System.currentTimeMillis();
        System.out.println("执行时长" + (end - start) + "毫秒");
    }
}
```

#### 记录日志

```java
package com.design.proxy;

public class Log implements Move {

    private Move move = null;

    public Log(Move move) {
        this.move = move;
    }

    public void move() {
        System.out.println("执行前记录日志");
        this.move.move();
        System.out.println("执行完记录日志");
    }
}
```

#### Main

```java
package com.design.proxy;

public class Main {

    public static void main(String[] args) {

        Car car = new Car();
        Time time = new Time(car);
        Log log = new Log(time);
        log.move();
    }
}

/**
 * 结果为
 * 执行前记录日志
 * 汽车行驶中
 * 执行时长0毫秒
 * 执行完记录日志
 */
```





