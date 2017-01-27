### 解释器模式（Interpreter）

#### 上下文

```java
package com.design.interpreter;

public class Context {
}
```

#### 语法接口

```java
package com.design.interpreter;

public interface Expression {

    public Object interpret(Context context);
}
```

#### 非终结符表达是

```java
package com.design.interpreter;

public class NonterminalExpression implements Expression {

    @Override
    public Object interpret(Context context) {
        return null;
    }
}
```

#### 终结符表达式

```java
package com.design.interpreter;

public class TerminalExpression implements Expression {

    @Override
    public Object interpret(Context context) {
        return null;
    }
}
```



