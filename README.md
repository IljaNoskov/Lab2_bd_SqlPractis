# Lab2_bd_SqlPractis
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
```
