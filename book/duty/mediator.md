### 调停者模式（Mediator）

#### 调停者类

```java
package com.design.mediator;

import java.util.HashMap;
import java.util.Map;

public class Mediator {

    private Map<String, Department> map = null;

    public Mediator() {

        this.map = new HashMap<String, Department>();
    }

    public void command(String departName) {

        this.map.get(departName).selfAction();
    }

    public void register(String departName, Department department) {

        this.map.put(departName, department);
    }
}
```

#### 部门接口

```java
package com.design.mediator;

public interface Department {

    public void selfAction();
    public void outAction();
}
```

#### 设计部门

```java
package com.design.mediator;

public class Design implements Department {

    private Mediator mediator = null;

    public Design(Mediator mediator) {

        this.mediator = mediator;

        // 将自身注册为调停对象
        this.mediator.register("design", this);
    }

    @Override
    public void selfAction() {

        System.out.println("设计部门做本职工作");
    }

    @Override
    public void outAction() {

        System.out.println("找开发部门协同办公");

        this.mediator.command("development");
    }
}
```

#### 开发部门

```java
package com.design.mediator;

public class Development implements Department {

    private Mediator mediator = null;

    public Development(Mediator mediator) {

        this.mediator = mediator;

        // 将自身注册为调停对象
        this.mediator.register("development", this);
    }

    @Override
    public void selfAction() {

        System.out.println("开发部门做本职工作");
    }

    @Override
    public void outAction() {

        System.out.println("找设计部门协同办公");

        this.mediator.command("design");
    }
}
```

#### Main

```java
package com.design.mediator;

public class Main {

    public static void main(String[] args) {

        // 创建调停者
        Mediator mediator = new Mediator();

        // 实例化所有调停对象
        Design design = new Design(mediator);
        Development development = new Development(mediator);

        design.selfAction();
        design.outAction();

        System.out.println("----------------");

        development.selfAction();
        development.outAction();
    }
}
/**
 * 设计部门做本职工作
 * 找开发部门协同办公
 * 开发部门做本职工作
 * ----------------
 * 开发部门做本职工作
 * 找设计部门协同办公
 * 设计部门做本职工作
 */
```

