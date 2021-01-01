# Decorator Pattern in Spring

- https://blog.tratif.com/2018/04/12/decorating-spring-components/

```java
public class BasicProductService implements ProductService {

  private final ProductRepository productRepo;

  public BasicProductService(ProductRepository productRepo) {
    this.productRepo = productRepo;
  }

  @Override
  public Product createProduct(String productName) {
    // simplified implementation for brevity
    Product product = new Product(productName);
    productRepo.save(product);
    return product;
  }
}
```

```java
public class FullTextSearchIndexedDecorator implements ProductService {

  private final ProductService wrappedProductService;
  private final FullTextSearchIndexService fullTextSearchIndexService;

  public FullTextSearchIndexedDecorator(
      ProductService wrappedProductService,
      FullTextSearchIndexService fullTextSearchIndexService) {
    this.wrappedProductService = wrappedProductService;
    this.fullTextSearchIndexService = fullTextSearchIndexService;
  }

  @Override
  public Product createProduct(String productName) {
    Product product = wrappedProductService.createProduct(productName);
    fullTextSearchIndexService.index(product);
    return product;
  }
}
```

Multiple implementations of an interface in a single Spring context

```java
@Configuration
public class AppConfiguration {

  @Bean(name = "basicService")
  ProductService basicService(ProductRepository productRepository) {
    return new BasicProductService(productRepository);
  }

  @Bean(name = "decoratedService")
  ProductService decoratedService(
      @Qualifier("basicService") ProductService basicProductService,
      ElkFullTextSearchIndexService indexService) {
    return new FullTextIndexedDecorator(basicProductService, indexService);
  }

  @Bean
  ServiceRequiringDecoratedService serviceRequiringDecoratedService(
      @Qualifier("decoratedService") ProductService productService) {
    return new ServiceRequiringDecoratedService(productService);
  }

  @Bean
  ServiceRequiringBasicService serviceRequiringBasicService(
      @Qualifier("basicService") ProductService productService) {
    return new ServiceRequiringBasicService(productService);
  }
}
```

A single implementation of an interface in Spring context

- only the basic implementation is created as a bean, other components can use base implementation and decorate it if needed

```java
@Configuration
public class AppConfiguration {

  @Bean
  ProductService basicService(ProductRepository productRepository) {
    return new BasicProductService(productRepository);
  }

  @Bean
  ServiceRequiringDecoratedService serviceRequiringDecoratedService(
      ProductService productService,
      ElkFullTextSearchIndexService indexService) {
    ProductService decoratedProductService = new FullTextIndexedDecorator(productService, indexService);
    return new ServiceRequiringDecoratedService(decoratedProductService);
  }

  @Bean
  ServiceRequiringBasicService serviceRequiringBasicService(ProductService productService) {
    return new ServiceRequiringBasicService(productService);
  }
}
```

- only the decorated implementation is created as a bean, all other components which are using auto-wiring will get the decorated implementation

```java
@Configuration
public class AppConfiguration {

  @Bean
  ProductService decoratedService(
      ProductRepository productRepository,
      ElkFullTextSearchIndexService indexService) {
    ProductService productService = basicService(productRepository);
    return new FullTextIndexedDecorator(productService, indexService);
  }

  @Bean
  ServiceRequiringDecoratedService serviceRequiringDecoratedService(ProductService productService) {
    return new ServiceRequiringDecoratedService(productService);
  }
}
```
