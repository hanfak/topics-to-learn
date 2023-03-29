# Resuse vs Decoupling 

- Reuse is a good thing 
  - DRY 
  - no duplication 
  - One place to change things 
  - But not for everything and all the time, great for business logic
- The reusable something is, the less usable it is 
  - Need to decide how reusable without becoming useless 
  - This lead to more things being coupled to this reusable thing
  - Lead to better have some duplication than being coupled  
- Lead to microservice pattern & event driven
  - Decoupled but with duplication 
  - But what happens when there is some sort of change that needs to happen to all services (technology change)
    - side car pattern and service mesh 
      - DRY/coupling at the infrastructure/service/architectural level
## Links 

- https://www.youtube.com/watch?v=Mx4BoNyKesk Supporting Constant Change • Neal Ford • YOW! 2018
