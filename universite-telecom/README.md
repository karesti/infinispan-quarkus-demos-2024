## Quarkus Quickstart

* Run in dev mode
```bash
./mvnw quarkus:dev
```
* Uncomment lines for adding import
* Add a new endpoint to display entities
```java
    @GET
    @Path("/entity/{id}")
    @Produces(MediaType.APPLICATION_JSON)
    public MyEntity getEntity(Integer id) {
        return MyEntity.findById(id);
    }
```
* Build and run in prod
```bash
./mvnw clean install -DskipTests=true 
```
* Show error. Datasource default not configured
* Run Postgres
```bash
 podman run --name postgres -e POSTGRES_USER=username -e POSTGRES_PASSWORD=password -p 5432:5432 -v /var/lib/data -d postgres
```
* Configure application
```properties
%prod.quarkus.datasource.db-kind=postgresql
%prod.quarkus.datasource.username=username
%prod.quarkus.datasource.password=password
%prod.quarkus.datasource.jdbc.url=jdbc:postgresql://localhost/postgres
%prod.quarkus.datasource.jdbc.max-size=8
%prod.quarkus.datasource.jdbc.min-size=2

# 
quarkus.hibernate-orm.database.generation=drop-and-create
quarkus.hibernate-orm.sql-load-script=import.sql
```
* Build and run again

```bash
./mvnw clean install -Dnative=true
```
