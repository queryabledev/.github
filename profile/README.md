<p align="center">
  <a href="https://queryable.dev">
    <img src="./assets/queryable.png" alt="Queryable" width="360">
  </a>
</p>

<h1 align="center">Queryable</h1>

<p align="center">
  Annotation-driven REST APIs for Quarkus and Hibernate Panache.
</p>

<p align="center">
  <a href="https://queryable.dev">Website</a> ·
  <a href="https://github.com/queryabledev/queryable">Queryable repository</a> ·
  <a href="https://github.com/queryabledev/queryable-tutorial">Tutorial</a>
</p>

## What is Queryable?

Queryable removes repetitive REST and filtering code from Quarkus
applications. Developers describe searchable fields directly on their JPA
entities; Queryable turns those annotations into REST endpoints, filtering,
sorting and pagination.

The project currently evolves from:

- **Queryable 3.x** — a Maven plugin that generates editable Java REST
  controllers and Hibernate filters;
- **Queryable 4.x** — a Quarkus extension designed around the official
  `quarkus-hibernate-orm-rest-data-panache` APIs, build-time generation and CDI
  extension points.

## Main repositories

| Repository | Purpose |
| --- | --- |
| [queryable](https://github.com/queryabledev/queryable) | Core project, documentation and releases |
| [queryable-tutorial](https://github.com/queryabledev/queryable-tutorial) | End-to-end examples and introductory tutorial |

## Queryable 3

```xml
<dependency>
  <groupId>it.n-ess.queryable</groupId>
  <artifactId>queryable-maven-plugin</artifactId>
  <version>3.0.15</version>
</dependency>
```

Queryable 3 is useful when generated Java resources should remain visible and
directly editable in the application.

## Queryable 4 direction

Queryable 4 focuses on:

- Quarkus augmentation and bytecode generation;
- no generated source files to merge or regenerate;
- REST Data Panache for standard CRUD, `/count`, OpenAPI and transactions;
- Queryable's expressive collection filtering;
- CDI extension points in `service.filters` and `service.rs`;
- Quarkus-native authentication and authorization through
  `application.properties`;
- explicit lifecycle callbacks such as `@PrePersist`, `@PostPersist`,
  `@PreUpdate` and `@PostUpdate`.

Example:

```java
@Entity
@QRs("/api/developers")
@QOrderBy("surname asc")
public class Developer extends PanacheEntityBase {

    @UuidGenerator
    @Id
    @QList
    public String uuid;

    @QLike
    public String name;

    @QLike
    public String surname;

    @QList
    public String team_uuid;

    @QLogicalDelete
    public boolean active = true;
}
```

This model exposes standard CRUD and collection queries such as:

```text
GET /api/developers?like.surname=pi
GET /api/developers?obj.team_uuid=<uuid>
GET /api/developers?obj.active=false
```

## Get involved

Explore the [tutorial](https://github.com/queryabledev/queryable-tutorial),
open an issue in the [core repository](https://github.com/queryabledev/queryable/issues),
or follow the project at [queryable.dev](https://queryable.dev).

Queryable is open source under the Apache-2.0 license.
