# Лабораторная работа №2. Вариант 4. Выполнил Носков Илья 21ПИ1.

#### Задание 1. Создаём таблицы.
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
    operation_name VARCHAR(255) NoT NULL,
    plase VARCHAR(255) NOT NULL,
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
Я использовал PRIMARY KEY для всех id, которые у меня были, кроме id, которые указывают на больницы или же персонал из других таблиц (как в work_rez). Для всех остальных значений я просто написал "NOT NULL", так как какие либо ограничения более были бы избыточными. Ни уникальность, ни что либо ещё нам не нужно.
Также я пытался добавить к id ещё один параметр - AUTO_INCREMENT, но увы, у меня не получилось. Выдавало не понятную мне ошибку и попытка загуглить её решение не увенчалась успехом.

#### Задание 2. Заполняем таблицы
``` sql
INSERT INTO medical_staff
Values (001,	'Медина',	'Вознесенское',	14),
(002,	'Севастьянов',	'Навашино',	14),
(003,	'Бессонов',	'Выкса',	10),
(004,	'Губанов',	'Выкса',	10),
(005,	'Боева',	'Починки',	5);

INSERT INTO work_plase
Values (001,	'Районная больница',	'Вознесенское',	10),
(002,	'Травм. пункт',	'Выкса',	3),
(003,	'Больница',	'Навашино',	4),
(004,	'Род. дом',	'Вознесенское',	12),
(005,	'Больница',	'Починки',	4),
(006,	'Травм.пункт',	'Лукояново',	3);

Insert INTO operation_type
Values (001,	'Наложение гипса',	'Выкса',	2000,	18000),
(002,	'Блокада',	'Навашино',	10000,	14000),
(003,	'Инъекция поливитаминов',	'Навашино',	20000,	11000),
(004,	'Инъекция алоэ',	'Навашино',	12000,	11000),
(005,	'ЭКГ',	'Вознесенское',	115,	10000),
(006,	'УЗИ',	'Вознесенское',	20,	30000),
(007,	'Флюорография',	'Выкса',	1000,	5000);

InSert INTO work_rez
VALUES (51040, 'Понедельник', 001, 001, 007, 4, 20000),
(51041, 'Понедельник', 003, 003, 006, 1, 30000),
(51042, 'Понедельник', 004, 003, 004, 3, 33000),
(51043, 'Понедельник', 004, 005, 001, 2, 36000),
(51044, 'Понедельник', 004, 004, 006, 1, 30000),
(51045, 'Среда', 002, 002, 005, 3, 30000),
(51046, 'Четверг', 003, 006, 004, 4, 44000),
(51047, 'Четверг', 004, 006, 002, 1, 28000),
(51048, 'Четверг', 005, 003, 003, 4, 44000),
(51049, 'Пятница', 002, 004, 005, 1, 10000),
(51050, 'Пятница', 003, 006, 004, 2, 22000),
(51051, 'Пятница', 003, 003, 001, 2, 36000),
(51052, 'Пятница', 005, 003, 002, 1, 14000),
(51053, 'Суббота', 003, 002, 007, 2, 10000),
(51054, 'Суббота', 004, 006, 004, 1, 11000),
(51055, 'Суббота', 005, 005, 004, 2, 22000),
(51056, 'Суббота', 003, 006, 003, 2, 22000);
```

#### Задание 3. Выводим все строки каждой из таблиц.
Запросы на вывод таблицы медицинского персонала.
```sql
select * from medical_staff
```
И результаты вывода таблицы медицинского персонала.
|  id |  surname | addres | tax |
|---|---|---|---|
| 1 | Медина | Вознесенское | 14 |
| 2 | Севастьянов | Навашино | 14 |
| 3 | Бессонов | Выкса | 10 |
| 4 | Губанов | Выкса | 10 |
| 5 | Боева | Починки | 5 |

Запрос на вывод мест работы.
``` sql 
select * from work_plase
```
И результат вывода мест работы
|  id |  plase | addres | tax |
|---|---|---|---|
| 1 | Районная больница | Вознесенское | 10 |
| 2 | Травм. пункт | Выкса | 3 |
| 3 | Больница | Навашино | 4 |
| 4 | Род. дом | Вознесенское | 12 |
| 5 | Больница | Починки | 4 |
| 6 | Травм.пункт | Лукояново | 3 |

В этой таблице я заметил, что написание у травмпунктов разное и исправил у 6 места, добавив пробел запросом
```sql
UPDATE work_plase set plase='Травм. пункт' where id=6
```

Запрос на вывод типов операций.
```sql
select * from operation_type
```
И таблица для них.
| id | operation_name | plase | stocks | price |
|---|---|---|---|---|
| 1 | Наложение гипса | Выкса | 2000 |  18000 |
| 2 | Блокада | Навашино | 10000 | 14000 |
| 3 | Инъекция поливитаминов | Навашино | 20000 | 11000 |
| 4 | Инъекция алоэ | Навашино | 12000 | 11000 |
| 5 | ЭКГ | Вознесенское | 115 | 10000 |
| 6 | Узи | Вознесенское | 20 | 30000 |
| 7 | Флюорография  | Выкса | 1000 | 5000 |

Проверка последней таблицы - 
```sql
select * from work_rez
```

И результат. Увы, таблица слишком большая и переносить её как таблицу будет слишком долго. Скорее всего дальше все результаты будут исключительно скринами.

<img width="758" alt="image" src="https://user-images.githubusercontent.com/99073996/200358244-de8bc406-5994-4038-82c9-e9bd2d484b08.png">
<img width="763" alt="image" src="https://user-images.githubusercontent.com/99073996/200358338-0d8ed49e-1405-40ac-953a-9cc307d94202.png">

#### Задание 4. Уникальные выборки.
4.c)
Запрос.
```sql
select DISTINCT address From medical_staff
```
Результат.

<img width="102" alt="image" src="https://user-images.githubusercontent.com/99073996/200605483-b2d8c066-265f-4ed8-8567-e334e3c8281c.png">

4.d)
Запрос.
```sql
select DISTINCT plase From work_plase
```

Результат.

<img width="108" alt="image" src="https://user-images.githubusercontent.com/99073996/200606249-e3059e3a-f11e-4422-b9be-beedbfdf831d.png">

4.e)
Запрос.
```sql
select DISTINCT date From work_rez
```

Результат.

<img width="68" alt="image" src="https://user-images.githubusercontent.com/99073996/200606622-152818dd-ff2c-4ab0-9196-5f96d21ca27a.png">


#### Задание 5. Поиск
5.c)
Запрос.
```sql
select contract_id,date From work_rez
where payment>=14000
```
Результат.

<img width="468" alt="image" src="https://user-images.githubusercontent.com/99073996/200607671-a3b789b1-6d5c-46df-af4d-ac4c32b5c348.png">
<img width="427" alt="image" src="https://user-images.githubusercontent.com/99073996/200607776-33ccd465-21c4-49de-b6dd-ac076ab783d5.png">

5.d)
Запрос.
```sql
select tax From medical_staff
where address='Выкса' or address='Навашино'
```

Результат.

<img width="50" alt="image" src="https://user-images.githubusercontent.com/99073996/200608416-3f3c8665-067c-434e-9d96-e27876cb543b.png">

5.e)
Запрос.
```sql
select operation_name,price,plase From operation_type
where price>10000 and (operation_name like ('%Инъекция%'))
ORDER BY plase,price
```

Результат.

<img width="560" alt="image" src="https://user-images.githubusercontent.com/99073996/200609987-c53081b1-400a-42ec-abdd-810e978b771d.png">

