# JDBC Template

```java
//[... initialize ...]

        final SimpleDataSourceFactory simpleDataSourceFactory = new SimpleDataSourceFactory("com.mysql.jdbc.Driver");
        final DataSource dataSource = simpleDataSourceFactory.createDataSource(jdbcUrl, user, pass);
        jdbcTemplate = new JdbcTemplate(dataSource);

        final DataSourceTransactionManager transactionManager = new DataSourceTransactionManager(dataSource);
        transactionTemplate = new TransactionTemplate(transactionManager);
        transactionTemplate.setPropagationBehavior(TransactionDefinition.PROPAGATION_REQUIRES_NEW);

//[... and then ...]

        transactionTemplate.execute(new TransactionCallback<Object>() {
            @Override
            public Object doInTransaction(TransactionStatus status) {
                jdbcTemplate.execute(...)     // will be executed in transaction
            }
        }
```

## Stored procedures

- https://mkyong.com/spring-boot/spring-boot-jdbc-stored-procedure-examples/
- https://www.tutorialspoint.com/springjdbc/springjdbc_stored_procedure.htm