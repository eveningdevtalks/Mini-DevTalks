# SOLID PRINCIPLES

## Single Responsibility Principle

Class should only have one responsibility. Furthermore, it should only have one reason to change

```java
class Cake {
  private String color;
  private String design;
}

class CakeWriter {

  public void writeEnglishText(Cake cake, String text) {
    // Do your awesome writing on this cool cake
  }

  public void writeSinhalaText(Cake cake, String text) {
    // Do your awesome writing on this cool cake
  }
}
```

## Open-Closed Principle

Classes should be open for extension but closed for modification

If you thought upgrading `Cake` with flavour like this, may be this bring breaking changes to your exising codes.

```java
class Cake {
    private String color;
    private String design;
    private String flavour;
}
```

Instead of that, you can do this.
```java
class ChocolateCake extends Cake {
  private String flavour;
}
```

## Liskov Substitution Principle

Objects of a superclass shall be replaceable with objects of its subclasses without breaking the application. That requires the objects of your subclasses to behave in the same way as the objects of your superclass.

```
Let Φ(x) be a property provable about objects x of type T. Then Φ(y) should be true for objects y of type S where S is a subtype of T.
```

```java
class Cake {
  private String color;
  private String design;

  public void bake() {
    // DO bake in 300 F for 25 minutes
  }
}

class ChocolateCake extends Cake {

  @Override
  public void bake() {
    // DO bake in 350 F for 30 minutes
  }
}

class CoffeeCake extends Cake {

  @Override
  public void bake() {
    // Do bake in 250 F for 20 minutes
  }
}

class CakeBaker {
  public void bakeCake(Cake cake) {
    // Do anything you want
    cake.bake();
  }
}
```

## Interface Segregation Principle

Larger interfaces should be split into smaller ones.

You can start implementing a `CakeDesigner` like this.

```java
interface CakeDesigner {
  void decorateCake();

  void cutPieces(int pieces);

  void wrapCake();
}

class JasperCakes implements CakeDesigner {
  void decorateCake() {
    // Yes, I would love to do this
  }

  void cutPieces(int pieces) {
    // Well... I am not doing this
  }

  void wrapCake() {
    // Why not...
  }
}
```

But here `JasperCakes` doesn't want to do `cutPieces`. That is wrong abstraction.

Instead of that, try this.

```java
interface CakeDecorator {
  void decorateCake();
}

interface CakePiecer {
  void cutPieces(int pieces);
}

interface CakeWrapper {
  void wrapCake();
}

class JasperCakes implements CakeDecorator, CakeWrapper {
  void decorateCake() {
    // Yes, I would love to do this
  }

  void wrapCake() {
    // Why not...
  }
}
```

## Dependency Inversion Principle

The decoupling of software modules, depends on abstractions. Instead of high-level modules depending on low-level modules, both will depend on abstractions.

```java
class UltimateCakeBaker {

  private ChocolateCake cake;

  public UltimateCakeBaker() {
    this.cake = new ChocolateCake();
  }

  public void bakeCake() {
    cake.bake();
  }
}

class UltimateCakeBaker {

  private Cake cake;

  public UltimateCakeBaker(Cake cake) {
    this.cake = cake;
  }

  public void bakeCake() {
    cake.bake();
  }
}
```

### An another example for dependency inversion principle.

```java
interface DBConnection {
  void connect();
}

class MySQLConnection implements DBConnection {
  void connect() {
    // Yeah.. This is mysql 👾
  }
}

class PostgreSQLConnection implements DBConnection {
  void connect() {
    // Yeah.. This is postgre 👽
  }
}

class MyApp {
  private final DBConnection connection;

  public MyApp(DBConnection connection){
    this.connection = connection;
  }

  public void connect() {
    connection.connect();
  }
}
```

You can simple create any instance of `MyApp` using any `DBConnection` type without having much effort.

```java
new MyApp(new MySQLConnection()).connect();
new MyApp(new PostgreSQLConnection()).connect();
```

Cheers!!

### Evening Dev Talks 🔥 03/06/2021