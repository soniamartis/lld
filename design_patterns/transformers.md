# Transformers

- Transfomer I
- Another pattern i have observed, that is used to pass around mutable state across multiple classes
- Once all the classes have transformed this mutable state, it is finally used for carrying out some processing
- Used in open api generation, where we require multiple transformations to the input file

```java
interface OpenApiTransfomer{
   TransformerContext transform(TransformerContext ctx);
}

class TransfomerContext{
  // a mutable object having state that can be mutated
}

class TransformerChain implements OpenApiTransfomer{

  List<OpenApiTransformer> transfomers;

  TransformerChain(){
   transformers = List.of(transformer1, transformer2, etc,);
 }

  TransformerContext transform(TransformerContext ctx){
    for(OpenApiTransfomer transformer: transfomers){
     ctx = transformer.transform(ctx);
   }

   return ctx;
   
  }
    
}


```

- Transformer II
- Do not pass around mutable state and define an input/output for each task
- Passing around a mutable object and modifying its state can have implications that may be hard to debug
- Instead define an Input and Output for each task and use the output of a task for generating the input of the next task
- This eliminates passing around of state, but the tasks can no longer be executed as a list, as they will now take in a diff input and return a diff output

```java
class Task1{
  public record Input(int x, int y){}

  public record Output(int a, int b){}

  public void runTask(Input input){
    //do something here with inputs
    return new Output(a,b);
 }
}

class Task2{
  Task1 task1;
 
  public record Input(int x, int y){}

  public record Output(int a, int b){}

  public void runTask(Input input){
    //do something here with inputs
    Task1.Output op = task1.runTask(new Task1.Input(x,y));
    // do something with task1's output
    return new Output(a,b);
 }
}



``` 
