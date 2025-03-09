# Adapter Pattern


- Proxy : object :: adapter : interface
- It is used as an adapter between 2 incompatible libraries
- Eg, Suppose there are 2 ppl, one speaks english and the other french, in order, for them to understand each other, we need a translator, who plays the role of an adapter
- A good example of the application of adapter pattern, is to build a wrapper around third party libraries, so that the client code does not depend directly on the library, rather on the adapter that wraps over the lib
- eg: etfdetails service client on top of etfdetails client

```java
// third party lib code
class LegacyPrinter {

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
