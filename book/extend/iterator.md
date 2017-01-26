### 迭代器模式（Iterator）

#### 迭代器接口

```java
package com.design.iterator;

public interface MyIterator {

    public void first();
    public void next();
    public boolean hasNext();
    public boolean isFirst();
    public boolean isLast();

    public Object getCurrent();
}
```

#### 实现类

```java
package com.design.iterator;

import java.util.ArrayList;
import java.util.List;

public class ConcreteMyAggregation {

    private List<Object> list = null;

    public ConcreteMyAggregation() {
        this.list = new ArrayList<Object>();
    }

    public List<Object> getList() {
        return this.list;
    }

    public void addList(Object object) {
        this.list.add(object);
    }

    public void removeList(Object object) {
        this.list.remove(object);
    }

    public MyIterator createMyIterator() {
        return new ConcreteMyIterator();
    }

    // 内部类
    private class ConcreteMyIterator implements MyIterator {

        private int current = 0;

        @Override
        public void first() {
            this.current = 0;
        }

        @Override
        public void next() {
            this.current++;
        }

        @Override
        public boolean hasNext() {
            return this.current < ConcreteMyAggregation.this.list.size();
        }

        @Override
        public boolean isFirst() {
            return this.current == 0;
        }

        @Override
        public boolean isLast() {
            return this.current == ConcreteMyAggregation.this.list.size() - 1;
        }

        @Override
        public Object getCurrent() {
            return ConcreteMyAggregation.this.list.get(this.current);
        }
    }
}
```

#### Main

```java
package com.design.iterator;

public class Main {

    public static void main(String[] args) {

        ConcreteMyAggregation list = new ConcreteMyAggregation();
        list.addList("aa");
        list.addList("bb");
        list.addList("cc");

        MyIterator myIterator = list.createMyIterator();

        while (myIterator.hasNext()) {
            System.out.println(myIterator.getCurrent());
            myIterator.next();
        }
    }
}
/**
 * 结果为
 * aa
 * bb
 * cc
 */
```



