### 备忘录模式(Memento)

备忘录模式的核心是拷贝对象内部的状态，这样就能将对象恢复到之前的状态

#### 例子

#### 文本类

```java
package com.design.memento;

public class Text {

    public String text = "";

    public Text(String text) {

        this.text = text;
    }

    public Memento memento() {
        return new Memento(this);
    }

    public void recovery(Memento memento) {
        this.text = memento.getText().text;
    }

}
```

#### 备案类

```java
package com.design.memento;

public class Memento {

    private Text text = null;

    public Memento(Text text) {
        this.text = new Text(text.text);
    }

    public void setText(Text text) {

        this.text = new Text(text.text);
    }

    public Text getText() {

        return this.text;
    }
}
```

#### Main

```java
package com.design.memento;

public class Main {

    public static void main(String[] args) {

        Text text = new Text("文本");

        System.out.println(text.text);

        Memento memento = text.memento();

        text.text = "更新文本";

        System.out.println(text.text);

        text.recovery(memento);

        System.out.println(text.text);
     }
}
/**
 * 结果为
 * 文本
 * 更新文本
 * 文本
 */
```

