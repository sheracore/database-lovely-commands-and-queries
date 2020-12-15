## Postgresql
### What is constraint: It's combination of columns that all of them together  should be uniq.
#### When creating table
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
## Foreign table
### Creating foreign table from another server that is conneted
```
create foreign table mtn_huawei_lte_cell_hrly_r7r8 () inherits(mtn_huawei_lte_cell_hrly) server master_server;
```

## Clickhouse
#### How to copy data from csv file to the clickhouse table
```
clickhouse-client --format_csv_delimiter="," --query="INSERT INTO rpat.mtn_transmission_mapping (region, province, city,device_name,resource_name,type,port_level, capacity, subtype,link_name) FORMAT CSV" < /tmp/mapping_2020_10_04.csv
```
## Mysql
### Export table csv format: 
```
mysql -h 192.168.*.* -u root -p  -e 'select * from rpat.mtn_2g_targets_2020_quarter4_health_index' > mtn_2g_targets_2020_quarter4_health_index.csv
```
