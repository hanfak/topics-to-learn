# Spring Data Repositories

## How

- Using annotated entity, we create an interface:

```java
@Entity
public class Author {
  @Id
  @GeneratedValue(strategy = GenerationType.AUTO)
  private Long id;

  private String firstName;
  private String lastName;
  @ManyToMany(mappedBy = "authors")
  private Set<Book> books;

  public Author() {
  }

  public Author(String firstName, String lastName, Set<Book> books) {...}

  // Omitted setters/getter/equals/hashcode/toString
}

public interface AuthorRepository extends CrudRepository<Author, Long>{}
```
- This CrudRepository interface provides several CRUD operations, and Spring will provide the implementation for us to use.
- Initialiasing with data
  - Use of `CommandLineRunner` which has a runnable
    - Spring will find any of these impementations and run them
    - Can be used as a main method
  - Can inject repository created, and use crud methods to add data or get data etc
