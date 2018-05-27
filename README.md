# accessAndMySQLTransfer

access2mysql.ipynb - convert Access MDB to MySQL

mysql2access.ipynb -  convert MySQL to Access MDB

Notice:

If your encoding is utf8mb4 and encounter problems when you run mysql2access.ipynb, please check that whether the table reported by mysql2access.ipynb includes varchar(255). If so, please revise it to varchar(191)

Change table name from lowercase to upper case
```python
with open('cbdb_data_new.sql', 'wt') as f:
    with open('cbdb_data.sql', 'rt') as f2:
        for line in f2:
            if 'TABLE' in line or 'INSERT INTO' in line:
                line = line.split('`')
                line[1] = line[1].upper()
                f.write('`'.join(line))
            else:
                f.write(line)
```

执行如下命令添加索引
```sql
alter table `BIOG_INST_DATA` change `tts_sysno` `tts_sysno` int primary key auto_increment;
```
