# Annotations
GCM brings support for annotations. 
Currently, only one class-level annotation is supported: *timeSensitivity*. 
In future versions, we will add more and more annotations. 

This is how the timeSensitivity for a type of node can be defined using GCM annotations:
```java
class Building {
    @timeSensitivity = (3,5)
}
```

The GCM generator will generate the following:
```java
class Building {
  @Override
  public void init() {
    setTimeSensitivity(3, 5);
  }
}
```