# Lab2_bd_SqlPractis

#### Создаём таблицы
```sql
CREATE TABLE medical_staff
(
    id int PRIMARY KEY,
    surname VARCHAR(255) NOT NULL,
    address VARCHAR(255) NOT NULL,
    tax int CHECK(tax<=100)
);

CREATE TABLE work_plase
(
    id int PRIMARY KEY,
    plase VARCHAR(255) NOT NULL,
    address VARCHAR(255) NOT NULL,
    tax int CHECK(tax<=100)
);

CREATE TABLE operation_type
(
    id int PRIMARY KEY,
    operation_name VARCHAR(255), NoT NULL
    plase VARCHAR(255) NOT NULL,
    address VARCHAR(255) NOT NULL,
    stocks int Not NULL,
    price int Not NULL
);	

CREATE TABLE work_rez
(
  contract_id int PRIMARY KEY,
  date VARCHAR(31) NOt NULL,
  worker_id int NOt NULL,
  plase_id int NOt NULL,
  operation_id int NOt NULL,
  operation_num int NoT NULL,
  payment int NOT NULL
);

```
