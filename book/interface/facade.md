### 外观模式(Facade)

在实际的开发中，有时候我们需要依次执行A，B，C三个函数，这样我们会写出很多这样的代码

```java
A();
B();
C();
```

这样的坏处是，如果某天由于业务的问题，导致了执行的顺序发生了改变，我们就不得不改变很多地方的代码。这时候我们可以用外观模式在改变这种情况。

### 例子

在现实生活中，我们有时候会喝茶，一般的顺序为，`加水->烧水->放入茶叶->泡茶->喝茶`，我们依照这个例子来用代码实现

#### Water类

```java
package com.desgin.facade;

public class Water {

    public void addWater()
    {
        System.out.println("加水");
    }

    public void boilWater()
    {
        System.out.println("烧水");
    }
}
```

#### Tea类

```java
public class Tea {

    public void putTea(String tea) {
        System.out.println("放入" + tea);
    }

    public void makeTea() {
        System.out.println("泡茶");
    }

    public void drinkTea() {
        System.out.println("喝茶");
    }
}
```

这时候我们实现一个Facade类

```java
package com.desgin.facade;

import com.desgin.facade.Water;
import com.desgin.facade.Tea;

public class Facade {

    private Water water = null;
    private Tea tea = null;

    public Facade() {
        this.water = new Water();
        this.tea = new Tea();
    }

    public void drinkTea(String tea) {
        this.water.addWater();
        this.water.boilWater();
        this.tea.putTea(tea);
        this.tea.makeTea();
        this.tea.drinkTea();
    }
}
```

以后如果我们需要喝茶只需要实例化Facade类，然后调用drinkTea函数即可。就算以后喝茶的执行顺序发生了改变，我们可以直接修改Facade类drinkTea。