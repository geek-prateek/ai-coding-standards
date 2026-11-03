# Engine and ORM portability reminders

This skill is engine- and language-independent; its examples are *illustrative*, not commands to copy blindly.

## Relational engines

- **PostgreSQL:** examine `EXPLAIN (ANALYZE, BUFFERS)` on authorized non-production/appropriate environments; `ANALYZE` executes the query, including side effects for writes. Understand transaction/locking context. Check collations, NULL ordering and index support.
- **SQL Server:** use appropriate execution plans and actual I/O/time tooling in a safe environment; ORM LINQ translation and parameter sniffing may affect plans. Isolation and clustered/nonclustered indexes differ from other engines.
- **MySQL/MariaDB:** inspect engine/version and explain capabilities; isolation defaults, collation and composite index behavior matter.
- **SQLite:** assess file locking, query planner and deployment footprint; often differs from a remote server DB.
- **Other SQL engines:** confirm pagination, index options, window functions, `RETURNING`, and transactional DDL before use.

## Document databases

For MongoDB and similar engines, inspect access patterns and indexes, projections, aggregation pipeline shape, document fan-out, and cursor semantics. Relational join guidance does not automatically apply. Avoid unbounded collection scans and large document retrieval if a narrower query is sufficient.

## ORM/query builder

- **Entity Framework / EF Core:** inspect LINQ-to-SQL translation, `ToList`/`AsEnumerable` boundaries, `Include`, split/single-query choice, lazy loading, tracking, projection, and version-specific capabilities. EF behavior varies by provider/version.
- **Hibernate/JPA:** inspect lazy relationships, fetch joins, batch fetching, entity graphs, session scope and pagination interaction.
- **Django ORM:** inspect `select_related`, `prefetch_related`, `.values()`, querysets' laziness and database-specific behavior.
- **SQLAlchemy:** inspect `selectinload`/`joinedload`/lazy loading, session identity map and query shapes.
- **Prisma / TypeORM / Sequelize:** examine generated SQL, `select/include`, loading strategy, pagination and transaction primitives supported by the installed version.

Never assume a feature or translation exists in the installed version. If the provider generates different SQL than expected, inspect the actual command before optimizing.
