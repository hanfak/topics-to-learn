# Sidecar

- Problem
  - Peripheral tasks such as Monitoring, Logging etc are critical to most applications and often integrated within them.
  - However, these tasks run alongside the same process as the application which is potentially inefficient and points to improper separation of concerns.
  - Plus, outages caused in these monitoring and logging components could severely impact the entire application functions.
- Solution
 - Co-locate as Sidecar
   - Uses
     - PRoxy
       - Egress traffic using https
       - Internal service traffic using https
   - How it works
     - Co-locate the set of tasks along with the application but place them in their process or container as a Sidecar
     - Sidecars are typically small/pluggable components and can be written in different languages
     - Both application and sidecar are deployed as a single unit, therefore latency is low
     - The sidecar can be used for modifying how the application container works without having to make any changes to the code
     - The sidecar is bolted to the application and its lifecycle is dependent on the application
     - If the sidecar container logic gets complex or tightly coupled with the main application, it may better be integrated with the main application’s code instead
   - example
     - A common example of the sidecar is the literal sidecar attached to a motorcycle — working as a single unit
     - The sidecar enhances the usability of the motorcycle by increasing passenger capacity
     - The sidecar could be made by another company and need not be bought from the motorcycle manufacturer — providing modularity and flexibility of choice
     - It does not have an engine of its own but relies on the engine of the actual motorcycle. If the motorcycle stops, the sidecar stops

##  Sidecar patterns

- Sidecar
- Adapter
- Ambassador

- https://matthewpalmer.net/kubernetes-app-developer/articles/multi-container-pod-design-patterns.html
