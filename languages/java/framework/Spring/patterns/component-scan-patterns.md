# Component Scan Patterns

## Hexagonal Architecture

- The core should have be framework agnostic, this can be hard to do in Spring
  - Will either have to 
    - Ignore the sterotypes (ie @Component) which can lead to even more spring stuff to inflitrate the domain
      - This can be a valid way, but most be strict, could use archunit to only allow sterotypes in the domain
    - Or Create Configuration files and beans, where you manually instantiate everything
- Instead you can use use component scan another way, by creating custom annotations (ie @Domain) inside the domain, and have the infrastructure do the mapping on those custom annotations to the component scan
  - limitations
    - If you need some conditional or profile-based bean construction, you will have to switch back to a bean factory.

### Links

- https://beyondxscratch.com/2019/07/28/domaindrivendesign-hexagonalarchitecture-tips-tricks-binding-the-domain-to-the-spring-context-with-componentscan/
- https://gitlab.com/beyondxscratch/hexagonal-architecture-java-springboot/-/tree/main?ref_type=heads