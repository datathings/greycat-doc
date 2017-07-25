# Getting started

As a first example, let's say your business domain consists of buildings and rooms.


# GCM file

A corresponding gcm-file could look like the following:  

``` java
class Building {
    att name : String
    rel rooms : Room
    ref address : Address
}
class Room {
    att name : String
    att size  : Integer
}
class Address {
    att street : String
    att houseNumber : Integer
    att plz : String
}
```      

This small example shows already the main concepts of GCM. 
It defines 3 different types: *Building*, *Room*, and *Address*. 
The type *Building* is defined by an attribute *name*, a relation *rooms* of type *Room*, and a reference *address* of type *Address*. 
The difference between a relation and a reference is the cardinality. 
A relation is basically a *to-many* relationship, whereas a reference is a *to-one* relationship. 
The API of the generated methods takes this into account.

# Generated code
The generated code for the above gcm-file looks like this:

Type *Building*:
``` java
public class Building extends BaseNode {
  public static final Meta META = new Meta("Building",-1366001964,-1366001964);
  public static final Meta ROOMS = new Meta("rooms", greycat.Type.RELATION, 108698360);
  public static final Meta ADDRESS = new Meta("address", greycat.Type.RELATION, -1147692044);
  public static final Meta NAME = new Meta("name", greycat.Type.STRING,3373707);

  public Building(long p_world, long p_time, long p_id, Graph p_graph) {
    super(p_world, p_time, p_id, p_graph);
  }

  public static Building create(long p_world, long p_time, Graph p_graph) {
    return (Building) p_graph.newTypedNode(p_world, p_time, Building.META.name);
  }

  public final void getRooms(Callback<Room[]> callback) {
    traverseAt(ROOMS.hash, new Callback<Node[]>() {
      @Override
      public void on(Node[] result) {
        if(result != null) {
          Room[] typedResult = new Room[result.length];
          System.arraycopy(result, 0, typedResult, 0, result.length);
          callback.on(typedResult);
        } else {
          callback.on(new Room[0]);
        }
      }
    });
  }

  public final Building addToRooms(Room value) {
    addToRelationAt(ROOMS.hash,value);
    return this;
  }

  public final Building removeFromRooms(Room value) {
    removeFromRelationAt(ROOMS.hash,value);
    return this;
  }

  public final void getAddress(Callback<Address> callback) {
    traverseAt(ADDRESS.hash, new Callback<Node[]>() {
      @Override
      public void on(Node[] result) {
        if(result != null && result.length == 1) {
          callback.on((Address)result[0]);
        } else {
          callback.on(null);
        }
      }
    });
  }

  public final Building setAddress(Address value) {
    ((Relation)this.getOrCreateAt(ADDRESS.hash, greycat.Type.RELATION)).clear().add(value.id());
    return this;
  }

  public final Building removeFromAddress(Address value) {
    removeFromRelationAt(ADDRESS.hash,value);
    return this;
  }

  public final String getName() {
    return (String) super.getAt(NAME.hash);
  }

  public final Building setName(String value) {
    setAt(NAME.hash,NAME.type, value);
    return this;
  }

  @Override
  public void init() {
  }

  @Override
  public int typeAt(int index) {
    return super.typeAt(index);
  }

  @Override
  public Object getAt(int index) {
    return super.getAt(index);
  }
}
```
  

Type *Address*:
``` java
public class Address extends BaseNode {
  public static final Meta META = new Meta("Address",516961236,516961236);
  public static final Meta STREET = new Meta("street", greycat.Type.STRING,-891990013);
  public static final Meta HOUSENUMBER = new Meta("houseNumber", greycat.Type.INT,1086437001);
  public static final Meta PLZ = new Meta("plz", greycat.Type.STRING,111102);

  public Address(long p_world, long p_time, long p_id, Graph p_graph) {
    super(p_world, p_time, p_id, p_graph);
  }

  public static Address create(long p_world, long p_time, Graph p_graph) {
    return (Address) p_graph.newTypedNode(p_world, p_time, Address.META.name);
  }

  public final String getStreet() {
    return (String) super.getAt(STREET.hash);
  }

  public final Address setStreet(String value) {
    setAt(STREET.hash,STREET.type, value);
    return this;
  }

  public final Integer getHouseNumber() {
    return (Integer) super.getAt(HOUSENUMBER.hash);
  }

  public final Address setHouseNumber(Integer value) {
    setAt(HOUSENUMBER.hash,HOUSENUMBER.type, value);
    return this;
  }

  public final String getPlz() {
    return (String) super.getAt(PLZ.hash);
  }

  public final Address setPlz(String value) {
    setAt(PLZ.hash,PLZ.type, value);
    return this;
  }

  @Override
  public void init() {
  }

  @Override
  public int typeAt(int index) {
    return super.typeAt(index);
  }

  @Override
  public Object getAt(int index) {
    return super.getAt(index);
  }
}
```

Type *Room*:
```java
public class Room extends BaseNode {
  public static final Meta META = new Meta("Room",2553083,2553083);
  public static final Meta SIZE = new Meta("size", greycat.Type.INT,3530753);
  public static final Meta NAME = new Meta("name", greycat.Type.STRING,3373707);

  public Room(long p_world, long p_time, long p_id, Graph p_graph) {
    super(p_world, p_time, p_id, p_graph);
  }

  public static Room create(long p_world, long p_time, Graph p_graph) {
    return (Room) p_graph.newTypedNode(p_world, p_time, Room.META.name);
  }

  public final Integer getSize() {
    return (Integer) super.getAt(SIZE.hash);
  }

  public final Room setSize(Integer value) {
    setAt(SIZE.hash,SIZE.type, value);
    return this;
  }

  public final String getName() {
    return (String) super.getAt(NAME.hash);
  }

  public final Room setName(String value) {
    setAt(NAME.hash,NAME.type, value);
    return this;
  }

  @Override
  public void init() {
  }

  @Override
  public int typeAt(int index) {
    return super.typeAt(index);
  }

  @Override
  public Object getAt(int index) {
    return super.getAt(index);
  }
}
```

As can be seen, besides the corresponding typed methods for getters and setters, the generated code also contains constants with meta information (e.g. name and type) for each property. 

# Creating a typed graph

