# mongodb replicatset

setup mongodb replicatset using docker compose

```sh
mongodump --uri="mongodb+srv://itscodingthing:kWh5XGGsXzZtcZbk@cluster0.bkuijyq.mongodb.net/" --archive --gzip | mongorestore --uri="mongodb://root:password@localhost:27021/" --archive --gzip --drop
```
