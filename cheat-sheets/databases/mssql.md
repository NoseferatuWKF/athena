sys tables
```sql
-- find all schemas
select name from sys.schemas;
-- find all tables
select name from sys.tables;
select TABLE_NAME from INFORMATION_SCHEMA.TABLES;
```

count all records in database
```sql
SELECT s.name, o.name,
  ddps.row_count 
FROM sys.indexes AS i
  INNER JOIN sys.objects AS o ON i.OBJECT_ID = o.OBJECT_ID
  INNER JOIN sys.dm_db_partition_stats AS ddps ON i.OBJECT_ID = ddps.OBJECT_ID
  INNER JOIN sys.schemas AS s ON o.schema_id = s.schema_id
  AND i.index_id = ddps.index_id 
WHERE i.index_id < 2  AND o.is_ms_shipped = 0 ORDER BY s.name, o.NAME
```

repeat query
```sql
insert into table (column1, column2)
values ('abc', 123)

go 100 -- n times of repeat
```

query multiple id
```sql
select * from table where id in (1, 2, 3)
```

declare and use variable
```sql
declare @find VARCHAR(30);
set @find = 'Man%';
select * from table where like @find
```

find all fk on table
```sql
exec sp_help 'TableName'
```

set database owner to create diagrams
```sql
exec sp_changedbowner 'sa';
```

add delete cascade on existing foreign key
```sql
alter table table_name drop constraint fk
go

alter table table_name with nocheck add constraint fk foreign key(id)
references fk_table (id) on delete cascade
go

alter table table_name check constraint fk
go
```

restore db from .bak
```sql
restore database [goportal-db-dev]
from disk = '/goportal-db-dev-2024-12-13-9-29.bak'
with replace,
move 'goportal-db-dev-2024-12-13-9-29_Data' to '/var/opt/mssql/data/goportal-db-dev.mdf',
move 'goportal-db-dev-2024-12-13-9-29_Log' to '/var/opt/mssql/data/goportal-db-dev_log.ldf'
go
```

explain query
```sql
SET SHOWPLAN_TEXT ON
SET SHOWPLAN_ALL ON
SET SHOWPLAN_XML ON
SET STATISTICS PROFILE ON
SET STATISTICS XML ON
```