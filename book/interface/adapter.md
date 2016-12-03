### 适配器模式(Adapter)

适配器模式就是用现有的类转换成`Client`所需要的接口，避免了重复开发。用我们现实中的例子来说，电视机需要用到三角插口，而我们的排插却是两脚的，这时候可以用转接口，让排插的两脚插口变成三角插口。

### 例子

现在`Client`需要一个学生接口，实现如下所示

```java
package com.design.adapter;

interface Student {
    public void study();
    public String name();
    public int age();
}
```

而其实我们早已经实现了一个`People`类，`People`类中已经实现了`name`函数和`age`函数，只是没有`study`函数

```java
package com.design.adapter;

public class People {
    public String name()
    {
        return "helbing";
    }

    public int age()
    {
        return 22;
    }
}
```

这时候我们可以创建一个适配器类来实现`Client`所需要的所有函数，适配器的写法有两种，一个基于类继承，一种是基于类对象。

#### 类继承写法

```java
package com.design.adapter;

import com.design.adapter.People;
import com.design.adapter.Student;

public class Adapter extends People implements Student {

    public void study() {
        System.out.println("Studying");
    }
}
```

#### 类对象写法

```java
package com.design.adapter;

import com.design.adapter.People;
import com.design.adapter.Student;

public class Adapter implements Student {

    private People people = new People();

    public void study() {
        System.out.println("Studying");
    }

    public String name() {
        return people.name();
    }

    public int age() {
        return people.age();
    }
}
```

