# Database Migrations - flywaydb

## What is it?

- Flyway is an open-source tool, licensed under Apache License 2.0, that helps you implement automated and version-based database migrations.
- It allows you to define the required update operations in an SQL script or as Java code.
- You can then run the migration from a command line client or automatically as part of your build process or integrated into your Java application.

- Maven
  - running locally
- Running as part of deployment via helm/kubernetes
  - Part of pre install hook job as part of helm deployment
- Placeholders
- naming conventions
- rollbacks
- schema_version in database
- versioning
- checksums
  - stops old scripts being edited


## Links


- https://flywaydb.org/getstarted/
- https://flywaydb.org/documentation/
- https://technology.amis.nl/2016/04/11/continuous-delivery-database/
- https://technology.amis.nl/2016/04/15/blog-continuous-delivery-oracle-database-ii/
- https://technology.amis.nl/2016/04/22/continuous-delivery-oracle-database-iii/
- https://www.wlangiewicz.com/2017/07/03/flyway-database-migrations-best-practices/
- example http://bisaga.com/blog/tag/flyway/
-  https://thoughts-on-java.org/flyway-getting-started/
