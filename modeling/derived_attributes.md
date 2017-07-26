# Derived attributes
Derived attributes can be declared in GCM using constants in combination with tasks.

Let's consider the following example:
```java
class SmartCity {
    const derivedAtt : Task = executeExpression("x + y")

    att x : Double = 5.1
    att y : Double = 1.5

}
```

We declare a constant *derivedAtt* of type *Task* and assign it the default value *executeExpression("x + y")*.
So, how does this become a derived attribute?
In fact, the GCM generator generates methods overrating the default greycat *getAt* and *typeAt* methods, like follows:

```java
  @Override
  public int typeAt(int index) {
    if(index == -1350706364) {
      return DERIVEDATT.type;
    } else if(index == -312153240) {
      return LISTNODENAMES.type;
    }
    return super.typeAt(index);
  }

  @Override
  public Object getAt(int index) {
    if(index == -1350706364) {
      return DERIVEDATT.value;
    } else if(index == -312153240) {
      return LISTNODENAMES.value;
    }
    return super.getAt(index);
  }
```

These methods are called when the graph is traversed.
As a result, we can use the following code, i.e. use it as a derived property. 

```java
    smartCity.traverse(SmartCity.DERIVEDATT.name, new Callback<Double>() {
        public void on(Double i) {
            Assert.assertEquals("6.6", i + "");
        }
    });
``` 