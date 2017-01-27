### 构建者（Builder）

#### 宇宙飞船构建接口

```java
package com.design.builder;

public interface AirShipBuilder {

    public EngineModule buildEngine();
    public OrbitalModule buildOrbital();
}
```

#### 宇宙飞船装配接口

```java
package com.design.builder;

public interface AirShipDirector {

    public AirShip DirectAirShip();
}
```

#### 宇宙飞船构建类

```java
package com.design.builder;

public class MyAirShipBuilder implements AirShipBuilder {

    @Override
    public EngineModule buildEngine() {
        System.out.println("构建发动机");
        return new EngineModule("发动机");
    }

    @Override
    public OrbitalModule buildOrbital() {
        System.out.println("构建轨道舱");
        return new OrbitalModule("轨道舱");
    }
}
```

#### 宇宙飞船装配类

```java
package com.design.builder;

public class MyAirShipDirector implements AirShipDirector {

    private MyAirShipBuilder myAirShipBuilder = null;

    public MyAirShipDirector(MyAirShipBuilder myAirShipBuilder) {

        this.myAirShipBuilder = myAirShipBuilder;
    }

    @Override
    public AirShip DirectAirShip() {

        AirShip airShip = new AirShip();

        airShip.setEngineModule(this.myAirShipBuilder.buildEngine());
        airShip.setOrbitalModule(this.myAirShipBuilder.buildOrbital());

        return airShip;
    }
}
```

#### 宇宙飞船类

```java
package com.design.builder;

public class AirShip {

    private OrbitalModule orbitalModule = null;
    private EngineModule engineModule = null;

    public OrbitalModule getOrbitalModule() {
        return orbitalModule;
    }

    public void setOrbitalModule(OrbitalModule orbitalModule) {
        this.orbitalModule = orbitalModule;
    }

    public EngineModule getEngineModule() {
        return engineModule;
    }

    public void setEngineModule(EngineModule engineModule) {
        this.engineModule = engineModule;
    }
}
```

#### 引擎模块类

```java
package com.design.builder;

public class EngineModule {

    private String name = "";

    public EngineModule(String name) {

        this.name = name;
    }
}
```

#### 轨道舱模块类

```java
package com.design.builder;

public class OrbitalModule {

    private String name = "";

    public OrbitalModule(String name) {

        this.name = name;
    }
}
```

#### Main

```java
package com.design.builder;

public class Main {

    public static void main(String[] args) {

        AirShipDirector airShipDirector = new MyAirShipDirector(new MyAirShipBuilder());
        AirShip airShip = airShipDirector.DirectAirShip();
    }
}
```

