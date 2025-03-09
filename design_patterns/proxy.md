# Proxy Pattern

- Create a wrapper on top of an object and access the methods of the object via the wrapper.
- Useful to provide additional functionality on top of the object
- All access to the underlying object will happen via the proxy object

In below scenario, if we directly call realImge, it will always keep reading from disk, so we build a proxy on top of it, so that we load from disk only when its called the first time, later on, we will just have a reference to the image via its proxy.

```java
// Eg1:
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

```java
// Eg2: suppose we are unable to add methods to this class, as it is part of external library/ generated pojo

class Instrument {
  identifiers: Map<String, String>
}

// we can create a wrapper on top of it and write methods to get the attrs we are interested in
class Security {
  Instrument instrument;

  String getSedol(){
    instrument.getIdentifiers().get("sedol");
  }
  
}
