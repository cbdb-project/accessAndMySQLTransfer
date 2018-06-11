# accessAndMySQLTransfer

access2mysql.ipynb - convert Access MDB to MySQL

mysql2access.ipynb -  convert MySQL to Access MDB

Notice:

1. If your encoding is utf8mb4 and encounter problems when you run mysql2access.ipynb, please check that whether the table reported by mysql2access.ipynb includes varchar(255). If so, please revise it to varchar(191)

2. Change table name from lowercase to upper case
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

 &gt;=python3.5 version:
```
with open('cbdb_data_new.sql', 'wt', encoding="utf8") as f:
    with open('cbdb_data.sql', 'rt', encoding="utf8") as f2:
        for line in f2:
            if 'TABLE' in line or 'INSERT INTO' in line:
                line = line.split('`')
                line[1] = line[1].upper()
                f.write('`'.join(line))
            else:
                f.write(line)
```

3. if all the values of bool types became 1, please try to switch

type_name = type_name if type_name != 'BYTE' else 'SMALLINT'

and

type_name = type_name if type_name != 'BIT' else 'SMALLINT'

4. 执行如下命令添加索引(just for CBDB)
```sql
alter table `BIOG_INST_DATA` change `tts_sysno` `tts_sysno` int primary key auto_increment;
```
