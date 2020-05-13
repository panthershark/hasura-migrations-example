# Run the hasura server

```
yarn 
docker-compose up -d
```
If you need the console at any point, open http://localhost:8080/console


# How to test that we can apply sql and metadata separately

Run the following steps against the same db server. The docker-compose does not use a volume b/c this is a small example and there is no reasons to persist between starts or add orpahn volumes to your docker instance.

##### Bootstrap a basic db

This initializes a db and hasura to track a table

```
cd hasura0
hasura migrate apply
hasura metadata apply
```

##### Apply an additive sql update (adds a col)

```
cd hasura1
hasura migrate apply
hasura metadata apply
```

##### Apply a destructive sql update (rm and add a col)

```
cd hasura2
hasura migrate apply
hasura metadata apply
```

# How to add another use case

- copy the lastest example folder
- add a migration, update metadata, etc
- export metadata
- test from end to end by following the above instructions

```bash
cp -R hasuraN hasuraN+1
cd hasuraN+1
hasura migrate create migration_name

# write sql or update metadata

hasura metadata export
```