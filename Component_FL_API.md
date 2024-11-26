<p align="center">
  <img src="images/LernaAI.png" alt="Lerna AI" />
</p>

# Lerna AI Federated Learning Service
Lerna FL Service is a centralized orchestrator/aggregator for all
participators in a Lerna AI Machine Learning instance. In order to expose
value of each training held on edge devices, Lerna AI requires an
orchestrator to provide required data to edge devices and an aggregator
to combine data and prepare it for the next iteration of machine learning.

## Execution

FL-API is a Java Spring Boot Application and should be run as stand-alone app
or as a docker container.

## Configuration

Example of `application.properties` file.

```shell
####################   [Database/Hibernate Configuration]   ####################
spring.jpa.database=POSTGRESQL
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=none
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
spring.jpa.properties.hibernate.temp.use_jdbc_metadata_defaults=false
spring.jpa.properties.hibernate.physical_naming_strategy=org.hibernate.boot.model.naming.PhysicalNamingStrategyStandardImpl
spring.jpa.properties.hibernate.event.merge.entity_copy_observer=allow
spring.jpa.properties.hibernate.id.new_generator_mappings=true
spring.jpa.properties.javax.persistence.query.timeout=30000
spring.jpa.properties.javax.persistence.validation.mode=none
spring.datasource.url=jdbc:postgresql://localhost:5432/lerna?loginTimeout=30&connectTimeout=30&socketTimeout=30&stringtype=unspecified
spring.datasource.username=devuser
spring.datasource.password=devpass

####################                [Flyway]                ####################
flyway.enabled=true

####################                [Redis]                 ####################
spring.redis.host=localhost
spring.redis.port=6379
#spring.redis.password=

####################              [Application]             ####################
server.port=8080
app.config.admin.token=admin-token
app.config.jwt.secret=SecretMustBeAtLeast512BitLong123456789012345678901234567890123456789012345678901234567890
app.config.fl.scalingFactor=100000

app.config.mpcServer.host=url.to.mpc
app.config.mpcServer.port=31337
app.config.mpc.keyStore=/path/to/cert.jks
app.config.mpc.keyStorePassword=change-me
app.config.mpc.trustStore=/path/to/cert.jks
app.config.mpc.trustStorePassword=change-me

app.config.webhook.queueName=change-me

app.config.actionml.spark.master=change-me
app.config.actionml.spark.esNode=change-me
```

## Requires

- PostgreSQL Server
- MPC Service
- Redis

## Required by

 - Lerna SDK (REST API on port 8080)
 - Dashboard (REST API on port 8080)
 - External services

## References

[FL-API Repository](https://github.com/lerna-ai/fl-api)

[FL-API Readme File](https://github.com/lerna-ai/fl-api/blob/master/README.md)
