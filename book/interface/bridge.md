### 桥接模式(Bridge)

桥接模式是为了解决某个类具有两个或两个以上的维度变化，如果只是用继承将无法实现这种需要，或者使得设计变得相当臃肿。

### 例子

以论坛给用户发送消息为例子，论坛可以给用户发送手机短信，email等等，同时消息也分为紧急和一般等等

#### 发送类接口

```java
package com.com.design.bridge;

interface Send {

    public void send(String to, String content);
}
```

#### 手机发送类

```java
package com.com.design.bridge;

public class Phone implements Send {

    public void send(String to, String content) {
        System.out.println("给" + to + "发送手机，内容为" + content);
    }
}
```

#### 邮件发送类

```java
package com.com.design.bridge;

public class Email implements Send {

    public void send(String to, String content) {
        System.out.println("给" + to + "发送邮件，内容为" + content);
    }
}
```

#### 消息基类

```java
package com.com.design.bridge;

import java.lang.reflect.Method;

public class Info {
    private Object object = null;
    public String content = "";

    public Info(Object object) {
        this.object = object;
    }

    public void setContent(String content) {
        this.content = content;
    }

    public void run(String to) {
        try {
            Method method = this.object.getClass().getDeclaredMethod("send", String.class, String.class);
            method.invoke(this.object, to, this.content);
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}
```

#### 一般消息类

```java
package com.com.design.bridge;

public class CommonInfo extends Info {

    public CommonInfo(Object object) {
        super(object);
    }

    public void setContent(String content) {
        this.content = "(一般)" + content;
    }
}
```

#### 紧急消息类

```java
package com.com.design.bridge;

public class WarningInfo extends Info {

    public WarningInfo(Object object) {
        super(object);
    }

    public void setContent(String content) {
        this.content = "(紧急)" + content;
    }
}
```

#### Main

```java
package com.com.design.bridge;

public class Main {

    public static void main(String[] args) {
        // 初始化一个发送邮件的消息
        Info info = new CommonInfo(new Email());
        // 设置消息内容
        info.setContent("这是邮件消息");
        // 开始发送
        info.run("helbing");
    }
}
// 结果为
// 给helbing发送邮件，内容为(一般)这是邮件消息
```

