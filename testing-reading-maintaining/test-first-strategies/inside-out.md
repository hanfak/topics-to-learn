# Inside out

- focus on implementing the Domain Model before defining how it is going to be used by the external world.
- The way users (via User Interface) or other systems (via APIs, Messages) interact with the system is treated as a lesser concern.
- Leaving the user interface (gui/rest) to be done later

## Benefits

- Early validation of business requirements
  - Start coding from the domain model allows us to focus on the business rules straightaway, giving us an opportunity to uncover business inconsistencies, clarify requirements with more details, and validate assumptions.
  - Getting a quick feedback on important areas of the system is a risk mitigation strategy.
- Risk mitigation
  - Identifying and mitigating risks before building too much code minimises re-work and helps to keep the cost of the project down.
- Most valuable things first
  - domain model is most important, as it contains the business logic
- Volatile User Interface left to the end
  - User Interfaces are notorious to be volatile while business rules tend to change far less once they are defined

## Drawbacks

- wasted effort
  - Without the guidance of a well-defined and concrete need from the external world (being a user interface or API — delivery mechanism), we can easily build things that are not needed.
  - When we finally define the delivery mechanism and try to plug it in, we quickly realise that the backend does not exactly satisfies all the needs of the delivery mechanism
  - At this point we need to either write some plumbing code to connect both sides, change the backend or worse, compromise on the usability defined by the delivery mechanism so that we can reuse the code in the backend as is.
- Speculative development
  - We start thinking about all the different possibilities and the things our code should do. We try to make our domain model as robust and generic as possible. We want to explore and often go off on a tangent without realising it
  - The more we speculate, the more accidental complexity creeps in.
- Delayed feedback
  - Users or external systems consuming our APIs don’t care about our backend. We can only get feedback from them if we can provide something for them to use or access. It doesn’t matter what we do on the backend.
  -  If the user journey (via the user interface) or APIs are not suitable, our backend has no value.
  -  If the front-end or APIs are done after the domain model (backend), we will only get feedback when the whole feature is done and that is too late.
-  Coarse-grained development
  -  A great way to deliver software incrementally is to slice our features in thin vertical slices. This becomes very hard when we start from the domain model, as we are not writing code to satisfy a specific external need.
-  Rushed delivery mechanism
  - when the backend is done, developers are generally out of time or not so keen to work on the front-end
  - They end up rushing the front-end implementation causing two main problems: a) a bad user experience, b) lower quality standards when comparing to the backend, leading to a messy and difficult-to-maintain delivery mechanism.
- Impaired collaboration
  - Mobile, front-end and backend teams should not work in parallel while the APIs are not defined
  - Having backend developers defining APIs cause a lot of friction and re-work once mobile and front-end developers try to integrate their code.
- 
