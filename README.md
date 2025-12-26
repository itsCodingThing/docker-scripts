# docker-scripts

some important docker and docker compose related scripts

create db dump

```sh
mongodump --uri="" --archive="backup.gz" --gzip
```

restore from dump

```sh
mongorestore --uri="" --archive="backup.gz" --gzip
```

in both case if database has user and password use string with user and password
