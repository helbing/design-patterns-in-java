### 观察者模式(Observer)

观察者模式也是常用设计模式之一，当对象发生改变时，会自动通知其他对象，让它们做出相应的改变。比如		`Angularjs`的双向数据绑定就是观察者模式的变种。

### 例子

#### Observers

```java
package com.design.observer;

interface Observer {

    public void update(Subject subject);
}
```

#### Subject

```java
package com.design.observer;

import java.util.ArrayList;
import java.util.List;

public class Subject {

    private List<Observer> observers = new ArrayList<Observer>();

    /**
     * 添加观察者
     * @param observer
     */
    public void attach(Observer observer) {
        this.observers.add(observer);
    }

    /**
     * 删除观察者
     * @param observer
     */
    public void detach(Observer observer) {
        this.observers.remove(observer);
    }

    /**
     * 通知所有注册的观察者
     */
    protected void notifyObservers() {
        for (Observer observer : this.observers) {
            observer.update(this);
        }
    }
}
```

接下来我们以指挥官和士兵作为一个例子

#### Solider类

```java
package com.design.observer;

public class Soldier implements Observer {

    private String name = "";

    public Soldier(String name) {
        this.name = name;
    }

    public void update(Subject subject) {
        Commander commander = (Commander) subject;
        System.out.println("士兵" + this.name + "执行命令" + commander.command);
    }
}
```

#### Commander类

```java
package com.design.observer;

public class Commander extends Subject {

    protected String command = "";

    public void commandSoldiers(String command) {
        this.command = command;
        super.notifyObservers();
    }
}
```

#### Main

```java
package com.design.observer;

import com.design.adapter.People;

public class Main {

    public static void main(String[] args) {
        // 给指挥官一些士兵
        Commander commander = new Commander();
        commander.attach(new Soldier("张三"));
        commander.attach(new Soldier("李四"));
        commander.attach(new Soldier("王五"));

        // 指挥官指挥士兵
        commander.commandSoldiers("立正");
        commander.commandSoldiers("向左转");
        commander.commandSoldiers("向右转");
    }
}

/**
 * 结果为
 * 士兵张三执行命令立正
 * 士兵李四执行命令立正
 * 士兵王五执行命令立正
 * 士兵张三执行命令向左转
 * 士兵李四执行命令向左转
 * 士兵王五执行命令向左转
 * 士兵张三执行命令向右转
 * 士兵李四执行命令向右转
 * 士兵王五执行命令向右转
 */
```

