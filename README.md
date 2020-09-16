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
