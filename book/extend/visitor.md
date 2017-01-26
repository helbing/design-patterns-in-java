### 访问者模式（Visitor）

访问者模式是封装某些作用于某种数据结构中各元素的操作，它可以在不改变数据结构的前提下定义作用于这些元素的新的操作

### 例子

#### 游客接口

```java
package com.design.visitor;

public interface Visitor {

    // 声明了访问者能访问哪里
    public void visit(Library library);
    public void visit(Park park);
}
```

#### 游客接口实现

```java
package com.design.visitor;

public class ChinaVisitor implements Visitor {

    @Override
    public void visit(Library library) {
        library.doSomething();
    }

    @Override
    public void visit(Park park) {
        park.doSomething();
    }
}
```

#### 元素抽象类

```java
package com.design.visitor;

public abstract class Element {

    public abstract void accept(Visitor visitor);
  	// 具体实现方法
    public abstract void doSomething();
}
```

#### 图书馆

```java
package com.design.visitor;

public class Library extends Element {

    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }

    @Override
    public void doSomething() {
        System.out.println("访问图书馆");
    }
}
```

#### 公园

```java
package com.design.visitor;

public class Park extends Element {

    @Override
    public void accept(Visitor visitor) {
        // 可以在这里做权限控制
        visitor.visit(this);
    }

    @Override
    public void doSomething() {
        System.out.println("访问公园");
    }
}
```

#### Main

```java
package com.design.visitor;

public class Main {

    public static void main(String[] args) {

        Visitor visitor = new ChinaVisitor();

        visitor.visit(new Library());
        visitor.visit(new Park());
    }
}
/**
 * 结果为
 * 访问图书馆
 * 访问公园
 */
```



