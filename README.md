# spring-data-guide

## Spring Data JPA vs Data JDBC

- Spring Data JPA
  - ORM (Object-Relational Mapping) via Hibernate
  - JPQL (Java Persistence Query Language)
  - lazy loading, caching, dirty checking
  - via persistence context (EntityManager), also called 1st level cache
  - complex relationships (ManyToOne, ManyToMany)
  - access of any entity (not only root) possible via repository
  - run sql only on flush (sync persistence context with db)
    - end of transaction
    - entityManager.flush()

- Spring Data JDBC
  - simpler, no ORM
  - just SQL, no JPQL
  - no EntityManager
  - no lazy loading, no caching, no dirty checking
  - run sql statements directly (e.g. on save()), more control
  - just OneTo-relationships ([docu](https://docs.spring.io/spring-data/relational/reference/jdbc/mapping.html#jdbc.entity-persistence.types.referenced-entities))
  - no @OneToOne or @OneToMany annotation, just optional @MappedCollection ([docu](https://docs.spring.io/spring-data/relational/reference/jdbc/mapping.html#jdbc.entity-persistence.types))
  - no bidirectional relationships, only top-down
  - oriented by domain-driven design (DDD)
  - access via root entity in repository
  - always load whole aggregate (root + referenced entities)
  - check 
    - [docu](https://docs.spring.io/spring-data/relational/reference/jdbc/why.html)
    - [video](https://www.youtube.com/watch?v=AnIouYdwxo0)
  - examples:
    - [official examples](https://github.com/spring-projects/spring-data-examples/tree/main/jdbc)
    - [Dan Vega](https://github.com/danvega/blog-jdbc/tree/master)

## Transaction Options

- general
  - the methods in SimpleJpaRepository and SimpleJdbcRepository have transactional annotations
  - so flush is depending on business transaction (e.g. in service-class)

- declarative via @Transactional annotation
  - uses a proxy
  - only for public methods
  - call from outside, no self-invocation inside class
  
- programmatic via TransactionTemplate 
  - abstraction over PlatformTransactionManager
  - more control of transaction inside method 
  - via lambda expression

![Bild](/images/spring-data-access-options.drawio.png)