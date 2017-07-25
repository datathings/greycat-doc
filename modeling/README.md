# GreyCat modeling

Until now, nodes and relationships of our graph were generic, i.e. untyped. 
In complex applications, working with an untyped graph of generic nodes and relationships can quickly become cumbersome, difficult to maintain, and error prone.
Instead, you often want to use the concrete concepts of your domain as types of the nodes of your graph. With *GreyCat Modeling (GCM)* we provide a typing layer on top of the untyped GreyCat core.

GreyCat modeling (GCM) consists of a language module, a code generator, and different build tools (e.g. maven, gradle, command line interface) to execute the generator.
In a first step, all business types are defined in *.gcm files using a domain specific language. 
Based on this, the GreyCat generator generates for each defined type one class as node type. 

Then, graphs can be created using these types.

# GCM features 
Besides types, GCM allows to define additional features, like indexes, constants, or the time sensitivity for a certain type.
The following list depicts an overview of the provided features:  

# GCM language grammar




# Bigger example
 
 
  
 