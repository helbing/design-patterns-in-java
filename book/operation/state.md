### 状态模式(State)

状态模式就是通过改变对象的内部状态来改变对象的行为

#### 例子

#### State

```java
package com.design.State;

public abstract class State {

    public abstract int handle(Operation operation, int first, int second);
}
```

#### AddState

```java
package com.design.State;

public class AddState extends State {

    public int handle(Operation operation, int first, int second) {
        if (operation.getOperation().equals("ADD")) {
            return first + second;
        }
        // 状态转移
        operation.setState(new ReduceState());
        return operation.getState().handle(operation, first, second);
    }
}
```

#### ReduceState

```java
package com.design.State;

public class ReduceState extends State {

    public int handle(Operation operation, int first, int second) {
        if (operation.getOperation().equals("REDUCE")) {
            return first - second;
        }
        // 状态转移
        operation.setState(new Undefined());
        return operation.getState().handle(operation, first, second);
    }
}
```

#### UndefinedState

```java
package com.design.State;

public class UndefinedState extends State {

    public int handle(Operation operation, int first, int second) {
        System.out.println("The state is undefined");
        return 0;
    }
}
```

#### Operation

```java
package com.design.State;

public class Operation {

    private State state = null;
    private String operation = "";

    public Operation() {
        // 初始化状态
        this.state = new AddState();
    }

    public void setState(State state) {
        this.state = state;
    }

    public State getState() {
        return this.state;
    }

    public void setOperation(String operation) {
        this.operation = operation;
    }

    public String getOperation() {
        return this.operation;
    }

    public int operate(int first, int second) {
        return this.state.handle(this, first, second);
    }

    public void reset() {
        this.setState(new AddState());
    }
}
```

#### Main

```java
package com.design.State;

public class Main {

    public static void main(String[] args) {

        int result = 0;

        Operation operation = new Operation();
        operation.setOperation("REDUCE");
        result = operation.operate(2, 1);
        System.out.println(result);

        // 状态复位
        operation.reset();

        operation.setOperation("ADD");
        result = operation.operate(1, 2);
        System.out.println(result);
    }
}
/**
 * 结果为
 * 1
 * 3
 */
```

