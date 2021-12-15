# Non functional Attributes (Quality Attributes)

- infrastructure services can be well defined as a function, like providing disk space, or routing network messages.
  - Functional Attributes
- Non-functional attributes, on the other hand, describe the qualitative behavior of a system, rather than specific functionalities.
- Examples of non-functional attributes are:
  - Availability
  - Scalability
  - Reliability
  - Stability
  - Testability
  - Recoverability
- NFAs important for the successful implementation and use of an IT infrastructure,
  - but in projects, they rarely get the same attention as the functional services
- When NFAs are not meant they have a direct impact on the business
  - Slow to deploy features to customers
  - Cannot maintain and users experience more bugs
  - Regulations cannot be met, and fines and reputational damage occurs
  - User experience is slow, buggy or outdated, and users will leave to competitors (clients or employees)
- NFAs are  functional indeed, but they are not directly related to the primary functionalities of a system
  - Better term would be quality attributes
  - This leads to important stakeholders of a business (ones with money and influence) to not have the same feelings about NFAs and focus more on functionality.
    - They conisder NFAs as hygiene factor and taken for granted
    - They dont mention them, or state them explicitly
    - But they have expectations of them

### Non functional Requirements (NFRs)

- Architects and engineers job is to find out these NFRs
- the acceptance of a system is largely dependent on the implemented non-functional requirements.
  - A website can be very beautiful and functional, but if loading the site (performance, a non-functional requirement) takes 30 seconds, most customers are gone!
- A large part of the budget for building an infrastructure is usually spent in fulfilling non-functional requirements that are not always clearly defined
- Infrastructure delivers manyof the NFRs
  - Examples
    - An application using an IT infrastructure built with several single points of failure will probably not reach very high availability figures, no matter how well the application is built
    - when the IT infrastructure is not designed to be scalable, the applications built upon it cannot introduce scalability as an afterthought. Will need to redesign and reimplement a new infrastructure which can be costly
    - When an IT infrastructure is setup to be highly available, a badly designed application can make the end result highly unreliable
    - security flaws on the processes level can undo all
- not unusual to have conflicting non-functional requirements in a system
  - Example
    - security versus user friendliness.
      - Users expect highly secured systems, but really don’t want to be bothered by password changes, smart card authentication, and other annoying security measures.
    - performance and cost.
      - Getting a high-performance system usually means getting more and faster hardware, and using strict implementation rules (which takes time to do and dependent on needs high cost engineers)
- 
