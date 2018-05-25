# accessAndMySQLTransfer
access2mysql.ipynb - convert Access MDB to MySQL
mysql2access.ipynb -  convert MySQL to Access MDB

Notice:
If your encoding is utf8mb4 and encounter problems when you run mysql2access.ipynb, please check that whether the table reported by mysql2access.ipynb includes varchar(255). If so, please revise it to varchar(191)
