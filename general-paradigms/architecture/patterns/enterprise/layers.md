# Layering/organisation of code
- Used to break complex systems
- Dependency inversion
  - High layers uses lower layers, but lower layers are unaware who it's consumers are
## Need to decide
  - What layers to have
  - what the responsibility of each layer is (Separation of concerns)
## Why
  - Make code easier to read, navigate
  - Easier to change and extend
  - Reduce area of change, dependencies are minimised
  - The layers can be understood without understanding other layers
  - Layers can be substituted
  - Good place for standardisation (ie TCP/IP)
  - reuse of layers or lower abstraction
  - performant code can be separated
  - Easier to test
## negatives
  - Layers may not encapsulate all things well, and changes may lead to cascading effect
  - Can harm performance, as communication between layers often involves transformations
    - but having specific layers can improve efficiency
  - Lots of layers, can lead to complexity and indirection
## Patterns
  - Hexagonal/clean/ports and adapters
  -  vertical
## 3 main layers
### Presentation
  - UI or API
  - handle interaction between consumer and application
  - interept commands of the consumer into actions for the domain/business logic to act upon
### domain/business logic
  - use cases
  - This is the point of the system
  - applying calculations, rules, validations on inputs, stored data and data from other sources
  - Informing/sending data to other sources/applications
### Data source logic
  - communicating with other systems that carry out tasks on behalf of the application
  - databases, ftp, machines, apis, messaging, packages or libraries
## Communication of layers
  - This can be dependent and can be strict on informal
  - Strict
    - Only layer above can access layer below, and not any other layer
      - Even can go both ways, and no layer depends on each other
    - Must go through interfaces, so that it can change layers
    - data/objects passed from layer to another is only used communication (DTO) , data cannot be used in other layers  
  - informal involes these rules being relaxed
  - The more strict you are the more complex the system will be and is meant for complex systems
    - Starting off strict might be too much at the start, but eventually this strictness helps when dealing with complex systems and hence systems will need to be refactored to meet that need
      - or if the system to be built is going to be strict then build this in from the start (slower start but faster progress as you get into it)
  - Example
    - presentation layer will ask domain layer for some data, the domain layer will get it from the data source, and give it back in the form the presentation layer wants
## Dependencies
  - domain and data source layers should never depend on presentation
    - allows for different presentations to be used
  - domain and data sources can be strictly non dependent, but this can be a bit slack
