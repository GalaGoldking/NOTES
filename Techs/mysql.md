# Connecting to mysql db

mysql -u {username} -p'{password}' -h {remote server ip or name} -P {port} -D {DB name}

mysql -u root -p'root' -h 127.0.0.1 -P 3306 -D local

No space after '-p' flag

# See all tables

SHOW TABLES;

# See all databases

SHOW databases;

# Goind into database

use [DATABASE_NAME];

# Show everything from tables

SELECT * FROM [TABLE_NAME]
