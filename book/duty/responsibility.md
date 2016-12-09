### 职责链(Chain of Responsibility)

责任链模式是一种对象的行为模式。在责任链模式里，很多对象由每一个对象对其下家的引用而连接起来形成一条链。请求在这个链上传递，直到链上的某一个对象决定处理此请求。发出这个请求的客户端并不知道链上的哪一个对象最终处理这个请求，这使得系统可以在不影响客户端的情况下动态地重新组织和分配责任。

​																		———from 《JAVA与模式》

#### 例子

#### 审批类

```java
package com.design.responsibility;

public abstract class Approval {

    protected Approval handle = null;

    protected void setHandle(Approval handle) {
        this.handle = handle;
    }

    public abstract void approval(int price);

    public static Approval getResponsibility()
    {
        // 设置责任链
        Seller seller = new Seller();
        TeamLeader teamLeader = new TeamLeader();
        Manger manger = new Manger();

        seller.setHandle(teamLeader);
        teamLeader.setHandle(manger);

        return seller;
    }
}
```

#### Seller

```java
package com.design.responsibility;

public class Seller extends Approval {

    public void approval(int price) {
        if (price <= 500) {
            System.out.println("Seller审批通过了不大于500元的订单");
        } else {
            this.handle.approval(price);
        }
    }
}
```

#### TeamLeader

```java
package com.design.responsibility;

public class TeamLeader extends Approval {

    public void approval(int price) {
        if (price <= 3000) {
            System.out.println("TeamLeader审批通过了不大于3000元的订单");
        } else {
            this.handle.approval(price);
        }
    }
}
```

#### Manger

```java
package com.design.responsibility;

public class Manger extends Approval {

    public void approval(int price) {

        System.out.println("Manger审批通过了订单");
    }
}
```

#### Main

```java
package com.design.responsibility;;

public class Main {

    public static void main(String[] args) {

        Approval approval = Approval.getResponsibility();
        approval.approval(100);
        approval.approval(2800);
        approval.approval(100000);
    }
}

/**
 * Seller审批通过了大于500元的订单
 * TeamLeader审批通过了不大于3000元的订单
 * Manger审批通过了订单
 */
```



