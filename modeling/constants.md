# Constants
GCM can also be used to define global (project wide) and local (class wide) constants.

## Global constants
Global constants can be defined as a top level element, like this:
```java
const GLOBAL_CONSTANT : Double = 4.5
```

This defines a constant with name *GLOBAL_CONSTANT* of type *Double* with value *4.5*.

The GCM generator generates a class *Constants* containing all global constants, e.g.
```java
public final class Constants {
  public static final Double GLOBAL_CONSTANT = 4.5;
}

```

## Local constants
Similar to global constants, GCM can be used to define local constants:
```java
class Building extends ASuperType {
    const BUILDING_CONSTANT : String = "my constant"
}
```

The GCM generator generates the following code:
```java
public class Building extends ASuperType {
  public static final MetaConst<String> BUILDING_CONSTANT = new MetaConst<String>("BUILDING_CONSTANT", greycat.Type.STRING,458804431, "bla");
```