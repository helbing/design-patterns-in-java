### 原型模式(Prototype)

原型模式是为了防止对象重复处理化而造成多大的开销。原型模式要求对象实现一个可以“克隆”自身的接口，这样就可以通过复制一个实例对象本身来创建一个新的实例。

#### 例子

#### 原型类

```java
package com.design.prototype;

public class Prototype implements Cloneable {

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```

#### 羊类

```java
package com.design.prototype;

public class Sleep extends Prototype {

    private String name = "";

    public Sleep(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

#### Main

```java
package com.design.prototype;

public class Main {

    public static void main(String[] args) {


        try {
            Sleep sleep = new Sleep("羊");
            Sleep cloneSleep = (Sleep) sleep.clone();
            cloneSleep.setName("克隆羊");

            System.out.println(sleep.getName());
            System.out.println(cloneSleep.getName());

        } catch (CloneNotSupportedException exception) {
            System.out.println(exception.getMessage());
        }
    }
}
/**
 * 结果为
 * 羊
 * 克隆羊
 */
```



