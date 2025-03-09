# Registry Pattern

- Used to register some data in a central location

```java

class ValidationRegistry {

    List<ValidationDefinition> validationDefinitions;

    void register(ValidationDefinition definition){
       validationDefinitions.add(definition);
    }

    List<ValidationDefinition> getDefinitions(){
      return Collections.unmodifiableList(validationDefinitions);
    }
}

//interface to register definitions

interface ValidationDefinitionBinder{
  void bindTo(ValidationRegistry registry);
}

class ValidatorA implements ValidationDefinitionBinder{

   void bindTo(ValidationRegistry registry){
    List<ValidationDefinition> defs = List.of(...);
    defaultDefs.forEach(registry::add);
  }
}


```
