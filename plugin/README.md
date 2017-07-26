# Extending GreyCat

GreyCat can easily be extended to fit your needs using plugins. Plugins offer a modular way to define more advanced Nodes, new Types and Actions. Some Plugins are already available like the [Machine Learning Plugin](../ml/README.md) and others are currently under development.

## Using an Existing Plugin

### Declare the plugin

The first step when using a plugin is to declare to the graph that you will use it.

To declare the use of a Plugin, first make sure to add it as dependency to your current project.Then pass an instance of the class (from the Plugin you want to use) implementing the Plugin interface to the Graph Builder using ".withPlugin()".


```java
Graph g = new GraphBuilder()
	.withMemorySize(10000) //cache size before sync to disk
	.withPlugin(new MLPlugin())
	.withStorage(new LevelDBStorage("_db"))
	.build();
	
 g.connect(isConnected -> {
	doSomething();
	});
```

Note that more than one Plugin can be used with the graph as long as there is no conflict between them.

```java
Graph g = new GraphBuilder()
	.withMemorySize(10000) //cache size before sync to disk
	.withPlugin(new MLPlugin())
	.withPlugin(new MyPlugin())
	.withPlugin(new MyOtherPlugin())
	.withStorage(new LevelDBStorage("_db"))
	.build();
	
 g.connect(isConnected -> {
	doSomething();
	});
```

