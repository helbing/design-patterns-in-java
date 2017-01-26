### 合成模式(Composite)

#### 抽象杀毒接口

```java
package com.design.composite;

public interface AbstractFile {

    public void killVirus();
}
```

#### 图片杀毒

```java
package com.design.composite;

public class ImageFile implements AbstractFile {

    private String filename = "";

    public ImageFile(String filename) {
        this.filename = filename;
    }

    @Override
    public void killVirus() {
        System.out.println("对图片文件" + this.filename + "进行杀毒");
    }
}
```

#### 文本文件杀毒

```java
package com.design.composite;

public class TextFile implements AbstractFile {

    private String filename = "";

    public TextFile(String filename) {
        this.filename = filename;
    }

    @Override
    public void killVirus() {
        System.out.println("对文本文件" + this.filename + "进行杀毒");
    }
}
```

#### 文件夹杀毒

```java
package com.design.composite;

import java.util.ArrayList;
import java.util.List;

public class Folder implements AbstractFile {

    private String filename = "";
    private List<AbstractFile> list = null;

    public Folder(String filename) {
        this.filename = filename;
        this.list = new ArrayList<AbstractFile>();
    }

    @Override
    public void killVirus() {
        System.out.println("对文件夹" + this.filename + "进行杀毒");

        for (AbstractFile  file : this.list) {
            file.killVirus();
        }
    }

    public void add(AbstractFile file) {
        list.add(file);
    }

    public void remove(AbstractFile file) {
        list.remove(file);
    }

    public AbstractFile getChild(int index) {
        return this.list.get(index);
    }
}
```

#### Main

```java
package com.design.composite;

public class Main {

    public static void main(String[] args) {

         AbstractFile f2, f3;

        Folder f1 = new Folder("文件夹");
        f2 = new ImageFile("图片文件");
        f3 = new TextFile("文本文件");

        f1.add(f2);
        f1.add(f3);

        f1.killVirus();
    }
}
/**
 * 结果为
 * 对文件夹文件夹进行杀毒
 * 对图片文件图片文件进行杀毒
 * 对文本文件文本文件进行杀毒
 */
```



