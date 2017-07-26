# Default values
GCM allows for all built-in types to declare initial values. 

## Default values for built-in types
For all built-in types default values can be declared in the gcm-file like follows:

```java
class Coordinate {
    att x : Double = 5.1
    att y : Double = 1.5
}
```

As we have seen it already for constants, this declaration leads the GCM generator to generate init methods where this default value are set.
This means that whenever a new instance of type *Coordinate* is created by greycat, these values will be initialized accordingly.

Default values are also possible for complex built-in types, like maps, arrays, or trees:
```java
class Building extends ASuperType {
    att intArr : IntArray = (3,2,3)
    att stringArr : StringArray = ("a", "b", "c", "d")

    att l2lMap : LongToLongMap = ((1,1),(2,2),(3,3))
    att l2laMap : LongToLongArrayMap = ((1,1),(1,2),(1,3))
    att i2strMap : IntToStringMap = ((1,"1"),(2,"2"))

    att dm : DMatrix = ((0,0,1),(0,1,1))

    att ndTree : NDTree = ((0,1,2,3),1,(0,0,0,0),(5,5,5,5),(0.5,0.5,0.5,0.5))
}
```

As can be seen in these example declarations, the default values are specified in form of a list of lists. 

## Default values for Tasks
One specifically interesting point is the concept of constant tasks with default values.
Let's for example consider that in our application we want to regularly list the names of all nodes.
One elegant way to do this, is to use a global constant of type *Task* with a corresponding default value.
This can be seen in the following example: 

```java
const listNodeNames : Task = readIndex("nodes").name
```

Now, the task can be conveniently executed from the generated global constant class. 



   