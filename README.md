# spring-data-guide

## Spring Data JPA vs Data JDBC

- Spring Data JPA
  - ORM (Object-Relational Mapping) via Hibernate
  - JPQL (Java Persistence Query Language)
  - lazy loading, caching, dirty checking
  - complex relationships (ManyToOne, ManyToMany)
  - access any entity via repository

- Spring Data JDBC
  - simpler, no ORM
  - just SQL, no JPQL
  - no EntityManager
  - no lazy loading, no caching, no dirty checking
  - run sql statements directly
  - just OneTo-relationships ([docu](https://docs.spring.io/spring-data/relational/reference/jdbc/mapping.html#jdbc.entity-persistence.types.referenced-entities))
  - no bidirectional relationships, only top-down
  - oriented by domain-driven design (DDD)
  - access via root entity in repository
  - check [docu](https://docs.spring.io/spring-data/relational/reference/jdbc/why.html)

![Bild](/images/spring-data-access-options.drawio.png)