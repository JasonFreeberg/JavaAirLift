# JavaAirLift Presentation notes

- The env vars can't be SPRING_DATASOURCE_* in the initial configuration because of Spring's precedence rules.
  - If we used SPRING_DATASOURCE_* then Spring would always use those strings and we would never be able to connect to the H2 DB

```bash
psql --host=javaairliftdb.postgres.database.azure.com --port=5432 --username=freeberg101@javaairliftdb --dbname=postgres_demos
```
