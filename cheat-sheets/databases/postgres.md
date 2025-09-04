connect to db
```bash
psql postgresql://[user]:[password]@[host]:[port][...][/dbname]?[param=value&...]
```

restore dump from sql
```bash
psql -f /path/to/back.sql -U <user>
```

commands
```bash
\l # list dbs
\c # connect to db
\d # list tables
\q # quit
\x on # expanded display use \x auto for both table and expanded
\watch [SEC] # execute query every SEC seconds
\! clear # clear term
```

get number of connections
```SQL
select sum(numbackends) from pg_stat_database;
```

copy to/from
```sql
\copy table to /path/to/file.csv delimiter ',' csv quote '"';
\copy table from /path/to/file.csv delimiter ',' csv quote '"';
```

count all records in database
```sql
SELECT schemaname,relname,n_live_tup 
  FROM pg_stat_user_tables 
ORDER BY schemaname, n_live_tup DESC;
```

kill all connections
```sql
SELECT pg_terminate_backend(pid)
FROM pg_stat_activity
WHERE datname = 'your_database_name';
```

grant
```sql
--ACCESS DB
REVOKE CONNECT ON DATABASE <db-name> FROM user;
GRANT  CONNECT ON DATABASE <db-name> TO user;

--ACCESS SCHEMA
REVOKE ALL     ON SCHEMA public FROM user;
GRANT  USAGE   ON SCHEMA public TO user;

--ACCESS TABLES
REVOKE ALL ON ALL TABLES IN SCHEMA public FROM user ;
GRANT SELECT                         ON ALL TABLES IN SCHEMA public TO read_only ;
GRANT SELECT, INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public TO read_write ;
GRANT ALL                            ON ALL TABLES IN SCHEMA public TO admin ;
```