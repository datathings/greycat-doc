# Custom types

GCM allows to define custom types using the keyword *type*. 
A custom type is similar to what you can declare in GCM as a *class*. 
However, there are a few important differences.

First and most importantly, a custom type can only be referenced from other classes as an attribute, i.e. via *att*, as shown in the following example:
```java
type GPSPosition {
    att lat : Double
    att lng : Double
}

class Building {
    att location : GPSPosition
}
```

This has a major implication: the custom type is *embedded* in the encompassing class, meaning that access to the custom type is synchronous instead as for relations and references asynchronous.
Custom types can only contain attributes by themselves.

The following code shows what the GCM generator generates for a declared custom type:

```java
public class GPSPosition extends BaseCustomTypeSingle {

    private static final String LAT = "lat";
    private static final int LAT_H = HashHelper.hash(LAT);
    private static final String LNG = "lng";
    private static final int LNG_H = HashHelper.hash(LNG);

    public GPSPosition(EStructArray p_backend) {
        super(p_backend);
    }

    @Override
    public void init() {
    }

    public final double lat() {
        return (double) getAt(LAT_H);
    }

    public final double lng() {
        return (double) getAt(LNG_H);
    }

    public final void setPosition(final double lat, final double lng) {
        this._backend.estruct(DEF_NODE).setAt(LAT_H, Type.DOUBLE, lat).setAt(LNG_H, Type.DOUBLE, lng);
    }

    @Override
    public String toString() {
        return "position(" + lat() + "," + lng() + ")";
    }

}
``` 

Next, the following example how to work with custom types:

```java
    SmartCity smartCity = SmartCity.create(0, 0, graph);
    GPSPosition pos = smartCity.getLocation();
    Assert.assertNull(pos);

    pos = smartCity.getOrCreateLocation();
    pos.setLng(5.43d);
    pos.setLat(3.23d);
```