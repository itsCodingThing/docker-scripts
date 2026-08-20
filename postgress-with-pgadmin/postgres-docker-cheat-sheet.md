# PostgreSQL & Docker Command Cheat Sheet

A quick-reference guide for managing PostgreSQL databases running inside Docker containers.

---

## 🐋 Docker Container Management

### Enter Container Shell
Opens an interactive terminal inside the running container.
```bash
docker exec -it <container_name> bash
```
*Note: Use `sh` instead of `bash` if the container image is minimal (like Alpine Linux).*

### Run a New Postgres Container
Starts a brand new PostgreSQL instance.
```bash
docker run --name <container_name> -e POSTGRES_PASSWORD=<your_password> -d postgres
```

---

## 🗄️ Database Actions (From Host Terminal)

These commands run directly from your machine's terminal without manual logging into the container.

### Create a Database
```bash
docker exec -it <container_name> createdb -U postgres <database_name>
```

### Delete (Drop) a Database
```bash
docker exec -it <container_name> dropdb -U postgres <database_name>
```

---

## ⌨️ Entering the Interactive SQL Prompt (psql)

`psql` is the built-in command-line tool. It is automatically installed inside the Docker container.

### Connect to Default Database
```bash
docker exec -it <container_name> psql -U postgres
```

### Connect to a Specific Database Directly
```bash
docker exec -it <container_name> psql -U postgres -d <database_name>
```

---

## 🚀 Commands Inside the psql Prompt

Run these commands *after* you have connected to the `psql` prompt.

### Database Navigation
* **`\l`** : List all available databases.
* **`\c <database_name>`** : Switch (connect) to another database.
* **`\q`** : Exit the `psql` prompt and return to terminal.

### Table & Schema Inspection
* **`\dt`** : Print (list) all standard tables in the current database.
* **`\dt+`** : List tables with extra details (like size and descriptions).
* **`\d <table_name>`** : View structural details (columns, types, keys) of a specific table.
* **`\dn`** : List all schemas.

### Useful SQL Queries
* **Create a database:**
  ```sql
  CREATE DATABASE database_name;
  ```
* **Drop a database:**
  ```sql
  DROP DATABASE database_name;
  ```
* **Force disconnect users (Fixes "Database is being accessed by other users" error):**
  ```sql
  SELECT pg_terminate_backend(pg_stat_activity.pid)
  FROM pg_stat_activity
  WHERE pg_stat_activity.datname = 'your_database_name'
    AND pid <> pg_backend_pid();
  ```

---

## 🔗 Connection String Format

Use this format to connect external applications or tools to your database:

```text
postgresql://[user]:[password]@[host]:[port]/[database_name]
```

### Local Host Example
```text
postgresql://postgres:mypassword@localhost:5432/my_new_db
```

### Docker-to-Docker Example
```text
postgresql://postgres:mypassword@<postgres_container_name>:5432/my_new_db
```
