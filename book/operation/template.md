### 模板方法模式(Template)

模板方法模式就是规定一套固定的执行步骤，然后可以让每一个执行步骤根据业务做自定义处理

#### 例子

以喝饮料为例子，我们需要按照`煮水`，`泡制饮料`，`倒入杯中`，`加入调料`这么一套模板来执行，根据我们喝的饮料的不同，如茶，咖啡，每个执行步骤又存在着差异，这时候就可以使用模板方法模式。

#### 喝饮料抽象类

```java
package com.design.template;

abstract class Drink {

    public final void drinkTemplate() {
        this.boil();
        this.brew();
        this.cup();
        this.condiment();
    }

    private void boil() {
        System.out.println("煮沸水");
    }

    protected void brew() {
        System.out.println("冲泡饮料");
    }

    private void cup() {
        System.out.println("倒入杯子中");
    }

    protected void condiment() {
        System.out.println("加入调料");
    }
}
```

#### 喝咖啡

```java
package com.design.template;

public class Coffee extends Drink {

    protected void brew() {
        System.out.println("加入沸水冲泡咖啡");
    }

    protected void condiment() {
        System.out.println("加入糖和牛奶");
    }
}
```

#### Main

```java
package com.design.template;

public class Main {

    public static void main(String[] args) {

        Drink coffee = new Coffee();
        coffee.drinkTemplate();
    }
}
/**
 * 煮沸水
 * 加入沸水冲泡咖啡
 * 倒入杯子中
 * 加入糖和牛奶
 */
```





