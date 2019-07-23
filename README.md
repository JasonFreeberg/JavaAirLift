# JavaAirLift Presentation notes

- The env vars can't be SPRING_DATASOURCE_* in the initial configuration because of Spring's precedence rules.
  - If we used SPRING_DATASOURCE_* then Spring would always use those strings and we would never be able to connect to the H2 DB
- Use the commands below to confirm that the records are going to Postgres:

    ```bash
    psql --host=javaairliftdb.postgres.database.azure.com --port=5432 --username=freeberg101@javaairliftdb --dbname=postgres_demo
    SELECT * FROM product;
    ```

- Set `JAVA_OPTS` to start continuous flight recordings:

    ```bash
    -XX:StartFlightRecording=disk=true,name=continuous_recording,dumponexit=true,maxsize=1024m,maxage=1d
    ```

- And to dump the flight recording:

    ```bash
    jcmd <pid> JFR.dump name=continuous_recording filename="/home/recording1.jfr"
    ```

https://java-app-key-vault.vault.azure.net/secrets/POSTGRES-USERNAME/2999981b08ac4e0fa206d0efad0a1a2a
https://java-app-key-vault.vault.azure.net/secrets/POSTGRES-PASSWORD/8e49887cca16454d9da0ff43b44f19b2
https://java-app-key-vault.vault.azure.net/secrets/POSTGRES-URL/5731e65bb9974a469126290ed5549235