### 命令模式（Command）

命令模式是将请求封装为对象，从而使你可用不同的请求对客户进行参数化; 对请求排队或记录请求日志，以及支持可撤销的操作。

### 例子

#### 命令接口

```java
package com.design.command;

interface Command {

    public void execute();
}
```

#### 攻击命令

```java
package com.design.command;

public class AttackCommand implements Command {

    private Solider solider = null;

    public AttackCommand(Solider solider) {

        this.solider = solider;
    }

    @Override
    public void execute() {

        this.solider.action("攻击命令");
    }
}
```

#### 士兵类

```java
package com.design.command;

public class Solider {

    public void action(String command) {

        System.out.println("士兵执行" + command);
    }
}
```

#### 指挥官类

````java
package com.design.command;

public class Commander {

    private Command command = null;

    public Commander(Command command) {

        this.command = command;
    }

    public void call() {

        this.command.execute();
    }
}
````

#### Main

```java
package com.design.command;

public class Main {

    public static void main(String[] args) {

        Solider solider = new Solider();

        Command command = new AttackCommand(solider);

        Commander commander = new Commander(command);

        commander.call();
    }
}
/**
 * 士兵执行攻击命令
 */
```

