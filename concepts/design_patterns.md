# Light-weight design patterns to use in java

## Proxy pattern
- Create a wrapper on top of an object and access the methods of the object via the wrapper.
- Useful to provide additional functionality on top of the object
- All access to the underlying object will happen via the proxy object

In below scenario, if we directly call realImge, it will always keep reading from disk, so we build a proxy on top of it, so that we load from disk only when its called the first time, later on, we will just have a reference to the image via its proxy.

```
interface Image{
  void display();
}

class RealImage implements Image{

 String fileName;

 public RealImage(String fileName){
    this.fileName = fileName;
  }

  void display(){
    // loadFromDisk();
  }
}

class ProxyImage implements Image {
   RealImage realImage;
   String fileName;

  public ProxyImage(String fileName){
    this.fileName = fileName;
  }

   void display(){
    if(realImage == null){
      realImage = new RealImage();
    }
    realImage.display();
  }
 
}
```
## Adapter Pattern
- Proxy : object :: adapter : interface
- It is used as an adapter between 2 incompatible libraries
- Eg, Suppose there are 2 ppl, one speaks english and the other french, in order, for them to understand each other, we need a translator, who plays the role of an adapter
- A good example of the application of adapter pattern, is to build a wrapper around third party libraries, so that the client code does not depend directly on the library, rather on the adapter that wraps over the lib
- eg: etfdetails service client on top of etfdetails client

```
// third party lib code
class LegacyPrinter{

  void printDocument(){
    // do printing
  }
}
// our client code adapter impl
interface Printer {
  void print();
}

class PrinterAdapter implements Printer{
  LegacyPrinter legayPrinter;

  void print(){
    legacyPrinter.printDocument();
  }
}

```

## Resolving data based on an input using a consistent interface(not too many additional classes)

```
interface PositionsLoader{
    List<Position> loadPositions(PositionSource source);
}

class PositionsRefLoader implements PositionsLoader{
    loadPositions(PositionsSource source);
}

class PositionScenarioLoader implements PositionsLoader{
    loadPositions(PositionsSource source);
}
...

class CompositeLoader implements PositionsLoader{

  PositionsRefLoader refLoader;

  PositionScenarioLoader scenarioLoader;

   List<Position> loadPositions(PositionsSource source){
    switch(source.getSourceType()){
      case ETF_POSITIONS_REF -> refLoader.loadPositions();
      case POSITION_SCENARIO -> scenarioLoader.loadPositions();
      ...
    }
  }
   
}
```

Another similar approach but not using switches:

```

interface PositionsLoader{
    List<Position> loadPositions(PositionSource source);
    boolean isEligible(PositionSource source);
}

class PositionsRefLoader implements PositionsLoader{

   boolean isEligible(PositionSource source){
      return source.getType() == ETF_POSITIONS_REF;
    }

    loadPositions(PositionsSource source){}
}

class PositionScenarioLoader implements PositionsLoader{

    boolean isEligible(PositionSource source){
      return source.getType() == POSITION_SCENARIO;
    }

    loadPositions(PositionsSource source){}
}

class CompositeLoader implements PositionsLoader{

  PositionsRefLoader refLoader;

  PositionScenarioLoader scenarioLoader;

  List<PositionLoader> loaders = List.of(refLoader, scenarioLoader);

   List<Position> loadPositions(PositionsSource source){
    PositionLoader eligibleLoader = loaders.filter(loader::isEligible).findFirst().orElse(() -> Exception);
    return eligibleLoader.loadPositions();
  }
   
}


```

  

  
