# Business and Data Layers Separation

- In a layered architecture or use of orms, there can be objects which are used in both business and data layers.
  - This leads to coupling of both layers
  - The Business layer should know nothing about the data layer and it's implementation. But by combing both layers (ie use of annotations or shared objects) it will.
  - This can lead to business objects, which have business logic and database logic
    - Breaking SRP
- To solve this is to use a mapping object, ie DAO.
  - So when business logic is finished with it's behaviour, it passes the object to the data layer by using another object
- Sharing Business and Data layers can be seen as a shortcut, and removal of duplication.
  - This is useful, for simple apps ie crud
  - but when the shared objects are used all over the place this can cause problems
