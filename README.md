# accessAndMySQLTransfer

access2mysql.ipynb - convert Access MDB to MySQL

mysql2access.ipynb -  convert MySQL to Access MDB

**We highly suggest you to use MySQL>=5.7**

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
```python
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


4. 情况operations表
operations包含操作记录，如果是需要删除请执行如下命令
```sql
TRUNCATE TABLE operations;
```

5. It must include drop table sentences, when you export MySQL datadump

6. If you copy some data from Access to a text file and then want to import that text file into MySQL, you have to replace FALSE by 0, and replace TRUE by 1 in that file

7. In CBDB, foreign key mechanism will stop you from truncating BIOG_MAIN. If you really want to update BIOG_MAIN only, you can: 1) delete the ids which you want to delete. 2) use REPLACE INTO instead of INSERT INTO to import your new data(**How to replace the data which were frozen by foreign keys**)

8. MySQL version<5.7 can define field type as JSON. If you are runing a MySQL<5.7, please don't import the tables below: operations, users

