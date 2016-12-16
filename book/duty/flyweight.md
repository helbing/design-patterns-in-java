### 享元模式(Flyweight)

在一些业务中需要创建很多相同的对象，这时候可以使用享元模式，直接返回已有的对象，防止重复创建对象。

JAVA中的Sring就是使用了享元模式

```java
String a = "123";
String b = a;
System.out.println(a==b);
```

上面的例子中结果为：true ，这就说明a和b两个引用都指向了常量池中的同一个字符串常量"abc"。这样的设计避免了在创建N多相同对象时所产生的不必要的大量的资源消耗。

#### 例子

#### MyString

```java
package com.design.flyweight;

public class MyString {

    private String string = "";

    public MyString(String string) {
        this.string = string;
    }

    public String getString() {
        return this.string;
    }
}
```

#### MyStringFactory

```java
package com.design.flyweight;

import java.util.HashMap;

public class MyStringFactory {

    private static HashMap<Integer, MyString> map = new HashMap<Integer, MyString>();

    public static MyString getStringObject(String string) {
        int hashCode = string.hashCode();

        MyString myString = map.get(hashCode);

        if (myString == null) {
            myString = new MyString(string);
            map.put(hashCode, myString);
        }

        return myString;
    }
}
```

#### Main

```java
package com.design.flyweight;

public class Main {

    public static void main(String[] args) {

        MyString str1 = MyStringFactory.getStringObject("123");
        MyString str2 = MyStringFactory.getStringObject("123");
        MyString str3 = MyStringFactory.getStringObject("456");
        MyString str4 = MyStringFactory.getStringObject("456");

        System.out.println(str1.getString() + " = " + str2.getString() + " : " + (str1 == str2));
        System.out.println(str1.getString() + " = " + str3.getString() + " : " + (str1 == str3));
        System.out.println(str3.getString() + " = " + str4.getString() + " : " + (str3 == str4));
    }
}
/**
 * 123 = 123 : true
 * 123 = 456 : false
 * 456 = 456 : true
 */
```



