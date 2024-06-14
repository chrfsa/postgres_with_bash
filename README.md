I have two files with .csv extension and I'm going to move them to a SQL file. i used bash scripting to do it.
and to transfer our DB postgres to a file.sql i used:
``` 
pg_dump --clean --create --inserts --username=<username> students > students.sql
```



