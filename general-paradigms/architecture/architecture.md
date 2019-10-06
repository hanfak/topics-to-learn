# Architecture

Concerned with where to put things.

Now more important to know where dependencies flow.

Happy -> demilaturised zone <-> world yes

Happy <-> world No

Happy = core, use case, interfaces
demilaturised zone = adapters implement adapters
world = frameworks/db/entrypoints/libraries/file systems

Software architecture is basically all about managing dependencies between architecture elements. If the dependencies become a big ball of mud, the architecture becomes a big ball of mud.

The Domain is King


## Concerns to think about

- https://reflectoring.io/checklist-architecture-setup/

## Patterns

- Archetectural Patterns
  - Clean
  - hexagonal
  - ports/adapters
  - domain driven
  - layered
  - onion
  - Martin Fowler Patterns
  - Feature toggles
    - ie for new versions of api

## Used Patterns

- Avoid using frame works like Spring or Hibernate (esp use of annotations or xmls)
- Embedding web containers/servers into jar
- Have a single wiring page to new up objects (no dependency injection framework)
- Property files
- Use repository pattern, instead of hibernate, in control of how we persist data into databases

### Books and Links

-
http://blog.borud.no/2013/03/gorging-on-java-frameworks-and.html
- http://www.catonmat.net/blog/frameworks-dont-make-sense/
- http://www.sickenger.com/2013/02/11/hibernate-just-stop-it/
- https://samnewman.io/patterns/architectural/bff/
- https://www.viewfromthecodeface.com/portfolio/clean-code-hexagonal-architecture/
- https://www.thoughtworks.com/insights/blog/write-quality-mobile-apps-any-architecture?utm_source=linkedin&utm_medium=social&utm_campaign=technology


## Books and Links

- [Clean Arthitecture - Uncle Bob post](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html)
- Not used as still new, but highly thought of [serverless architecture] (https://martinfowler.com/articles/serverless.html)
- https://dzone.com/articles/layered-architecture-is-good
- https://dzone.com/articles/hexagonal-architecture-is-powerful
- https://dzone.com/articles/onion-architecture-is-interesting
- https://dzone.com/articles/package-by-feature-is-demanded
- https://dzone.com/articles/clean-architecture-is-screamings
- https://github.com/donnemartin/system-design-primer
- https://crosp.net/blog/software-architecture/clean-architecture-part-2-the-clean-architecture/
- https://crosp.net/blog/software-architecture/clean-architecture-part-1-databse-vs-domain/
- http://blog.cleancoder.com/uncle-bob/2016/01/04/ALittleArchitecture.html
- https://herbertograca.com/2017/07/03/the-software-architecture-chronicles/
- https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/
- https://geeks.uniplaces.com/putting-clean-architecture-into-practice-20c47d8c76de
- https://java-design-patterns.com/blog/build-maintainable-systems-with-hexagonal-architecture/
- http://www.thedigitalcatonline.com/blog/2016/11/14/clean-architectures-in-python-a-step-by-step-example/
- https://www.youtube.com/watch?v=CnailTcJV_U&list=WL&index=154&t=10s
- https://javadevguy.wordpress.com/2017/07/27/a-detailed-analysis-of-the-clean-architecture-from-an-object-oriented-perspective/
- https://www.freecodecamp.org/news/implementing-a-hexagonal-architecture/

### Books

- [Clean Architecture - uncle bob]()
- [Domain Driven Design - ]()
- [?? - Martin Fowler]()
