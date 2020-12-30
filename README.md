# DBMS

DBMS Language

To communicate database updates and queries, DBMS language is used. Different types of database languages are explained below:
* Data Definition Language (DDL): It is used to save information regarding tables schemas, indexes, columns, constraints, etc.
* Data Manipulation Language (DML): It is used for accessing and manipulating databases.
* Data Control Language (DCL): It is used to access the saved data. It also allows to give or revoke access from a user.
* Transaction Control Language (TCL): It is used to run or process the modifications made by the DML.



# Postgresql
### What is constraint: It's combination of columns that all of them together  should be unique.
#### This commands contain creating database and user and grant for all users
```
create database database_name
create user username with password 'password'
GRANT CONNECT ON DATABASE database_name TO username;
GRANT ALL PRIVILEGES ON DATABASE database_name TO username;
ALTER USER username CREATEDB;
```
#### Creating table
```
CREATE TABLE order_details
( order_detail_id integer CONSTRAINT order_details_pk PRIMARY KEY,
  order_id integer NOT NULL,
  order_date date,
  quantity integer,
  notes varchar(200),
  CONSTRAINT order_date_unique UNIQUE (order_id, order_date)
);
```
### Constraint
#### After creating table
```
ALTER TABLE table_name
ADD CONSTRAINT constraint_name UNIQUE (column1, column2, ... column_n);
```
#### And for droping constraint using this
```
ALTER TABLE table_name
DROP CONSTRAINT constraint_name;
```
#### To get max two column together you can use this function type
```
select max(date_tiem, formula_cal) from table;
```
#### How to dump from table into the local by csv format and reverse from local to date base
##### From table to local in csv format
```
COPY(select region,province, city,device_name,resource_name,type,port_level, capacity, subtype, link_name from mtn_transmission_mapping where deleted = false) to '/tmp/mapping_2020_10_04.csv' with  csv;
```
##### From csv file to table 
```
COPY(region,province, city,device_name,resource_name,type,port_level, capacity, subtype, link_name) from '/tmp/mapping_2020_10_04.csv' with  csv;
```
### Analyze
#### We can use two type of analyze 
```
expalin select ...
explain analyze select ....
```
### Foreign table
### Creating foreign table from another server that is conneted
```
create foreign table mtn_huawei_lte_cell_hrly_r7r8 () inherits(mtn_huawei_lte_cell_hrly) server master_server;
```
### Converting date to char
```
to_char(collection_date::Date, 'YYYY')
to_char(collection_date::Date, 'YYYY/mm/dd')
```

# Clickhouse
#### How to copy data from csv file to the clickhouse table
```
clickhouse-client --format_csv_delimiter="," --query="INSERT INTO rpat.mtn_transmission_mapping (region, province, city,device_name,resource_name,type,port_level, capacity, subtype,link_name) FORMAT CSV" < /tmp/mapping_2020_10_04.csv
```
### Buffer Table Engine
Buffers the data to write in RAM, periodically flushing it to another table. During the read operation, data is read from the buffer and the other table simultaneously.
```
Buffer(database, table, num_layers, min_time, max_time, min_rows, max_rows, min_bytes, max_bytes)
```
Engine parameters:

    database – Database name. Instead of the database name, you can use a constant expression that returns a string.
    table – Table to flush data to.
    num_layers – Parallelism layer. Physically, the table will be represented as num_layers of independent buffers. Recommended value: 16.
    min_time, max_time, min_rows, max_rows, min_bytes, and max_bytes – Conditions for flushing data from the buffer.

Data is flushed from the buffer and written to the destination table if all the min* conditions or at least one max* condition are met.

    min_time, max_time – Condition for the time in seconds from the moment of the first write to the buffer.
    min_rows, max_rows – Condition for the number of rows in the buffer.
    min_bytes, max_bytes – Condition for the number of bytes in the buffer.

During the write operation, data is inserted to a num_layers number of random buffers. Or, if the data part to insert is large enough (greater than max_rows or max_bytes), it is written directly to the destination table, omitting the buffer.

The conditions for flushing the data are calculated separately for each of the num_layers buffers. For example, if num_layers = 16 and max_bytes = 100000000, the maximum RAM consumption is 1.6 GB.

# Mysql
### Export table csv format: 
```
mysql -h 192.168.*.* -u root -p  -e 'select * from rpat.mtn_2g_targets_2020_quarter4_health_index' > mtn_2g_targets_2020_quarter4_health_index.csv
```
