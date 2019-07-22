# JavaAirLift Presentation notes

- The env vars can't be SPRING_DATASOURCE_* in the initial configuration because of Spring's precedence rules.
  - If we used SPRING_DATASOURCE_* then Spring would always use those strings and we would never be able to connect to the H2 DB

```bash
psql --host=javaairliftdb.postgres.database.azure.com --port=5432 --username=freeberg101@javaairliftdb --dbname=postgres_demo
SELECT * FROM product;
```

 az keyvault secret set --name POSTGRES-USERNAME --value $env:POSTGRES_USERNAME --vault-name java-app-key-vault
 az keyvault secret set --name POSTGRES-PASSWORD --value $env:POSTGRES_PASSWORD --vault-name java-app-key-vault
 az keyvault secret set --name POSTGRES-URL --value $env:POSTGRES_URL --vault-name java-app-key-vault

https://java-app-key-vault.vault.azure.net/secrets/POSTGRES-USERNAME/2999981b08ac4e0fa206d0efad0a1a2a
https://java-app-key-vault.vault.azure.net/secrets/POSTGRES-PASSWORD/8e49887cca16454d9da0ff43b44f19b2
https://java-app-key-vault.vault.azure.net/secrets/POSTGRES-URL/5731e65bb9974a469126290ed5549235