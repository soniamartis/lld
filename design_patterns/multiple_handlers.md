# Pattern to pick handler from available handlers

## Composite pattern I (named it by myself, used widely in spring)
- Use this pattern when u have several handlers to select from , and u need to pick a handler based on a certain input

```java
interface PositionsLoader {
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
- Another similar approach but keeping the eligibility criteria within it's handler

```java

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
 
  private final List<PositionLoader> loaders;

  public CompositeLoader(PositionsRefLoader refLoader, PositionScenarioLoader scenarioLoader){
    loaders = List.of(refLoader, scenarioLoader);
  }

   List<Position> loadPositions(PositionsSource source){
    PositionLoader eligibleLoader = loaders.filter(loader::isEligible).findFirst().orElse(() -> Exception);
    return eligibleLoader.loadPositions();
  }
   
}


```


## Composite pattern II
- This pattern is similar to the above, except that here, we cannot determine the exact handler based on input, rather, it depends on whether the handlers defined in the list could handle the request or not
- eg. used in security master service to find instrument in a source
- If data is available, then load from there and skip all other sources, else waterfall to the next available source

  
