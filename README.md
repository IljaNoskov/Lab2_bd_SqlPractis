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
Я использовал PRIMARY KEY для всех id, которые у меня были, кроме id, которые указывают на больницы или же персонал из других таблиц (как в work_rez). Также я использовал проверку того, что цифра не больше 100 для налогов Для всех остальных значений я просто написал "NOT NULL", так как какие либо ограничения более были бы избыточными. Ни уникальность, ни что либо ещё нам не нужно.
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


#### Задание 6. Вывод записей.
6.c)
Запрос.
```sql
select work_rez.date, medical_staff.surname, work_plase.plase, operation_type.operation_name from work_rez,medical_staff,work_plase,operation_type
where work_rez.worker_id=medical_staff.id and work_rez.plase_id=work_plase.id and work_rez.operation_id=operation_type.id
```
Результат.

<img width="755" alt="image" src="https://user-images.githubusercontent.com/99073996/200612426-98c974fa-1e36-4b91-93da-2d2fb21dfdca.png">
<img width="706" alt="image" src="https://user-images.githubusercontent.com/99073996/200612648-fe9e4d99-6fdc-4506-a302-ce8b5b0c43a7.png">

6.d)
Запрос.
```sql
select work_rez.contract_id, work_plase.plase, work_rez.operation_num,work_rez.payment from work_rez,work_plase
where work_rez.plase_id=work_plase.id
ORDER BY work_rez.payment
```
Результат.

<img width="625" alt="image" src="https://user-images.githubusercontent.com/99073996/200614195-94686f19-aa6f-43e8-bbd8-d59d92a1b97f.png">
<img width="617" alt="image" src="https://user-images.githubusercontent.com/99073996/200614349-b5759d06-d617-42a5-9278-80323ca2a210.png">



#### Задание 7.
7.с)
Запрос.
```sql
select medical_staff.surname,medical_staff.address from medical_staff,work_rez,operation_type
where medical_staff.id=work_rez.worker_id 
and work_rez.operation_id= operation_type.id 
and operation_type.operation_name='Наложение гипса'
and work_rez.operation_num>1
```
Результат.

<img width="423" alt="image" src="https://user-images.githubusercontent.com/99073996/200639081-72b6d00b-99f4-4ed8-a44a-267fcaf5fdae.png">

7.d)
Запрос.
```sql
select operation_type.operation_name from medical_staff,work_rez,work_plase,operation_type
where medical_staff.address in ('Вознесенское','Выкса')
and work_plase.plase='Больница'
and medical_staff.id=work_rez.worker_id
and work_rez.plase_id=work_plase.id
AND operation_type.id=work_rez.operation_id
```
Результат.

<img width="103" alt="image" src="https://user-images.githubusercontent.com/99073996/200640631-3ef29ade-32f7-4075-ae57-891941221aef.png">

7.e)
Запрос.
```sql
select work_plase.plase,work_plase.tax,medical_staff.surname from work_plase,medical_staff,work_rez
where medical_staff.id =work_rez.worker_id
and work_plase.id=work_rez.plase_id
and medical_staff.tax BETWEEN 7 and 16
Order BY work_plase.tax,medical_staff.tax
```
Результат.

<img width="741" alt="image" src="https://user-images.githubusercontent.com/99073996/200643850-fa896136-d8b4-48d7-b059-2c0e77b73924.png">
<img width="724" alt="image" src="https://user-images.githubusercontent.com/99073996/200643964-e19f44ac-963e-445f-85b5-068aafc3a19a.png">


7.a)
Запрос.
```sql
select work_rez.date,work_rez.operation_id,medical_staff.surname from work_rez,medical_staff
where medical_staff.id=work_rez.worker_id
and work_rez.payment>7000
and work_rez.operation_num>1
```
Результат.

<img width="565" alt="image" src="https://user-images.githubusercontent.com/99073996/200644851-3e4f81a0-4b91-4833-927f-47998a217b39.png">


####Задание 8.
Сейчас поменяются скрины, так как я пересел с ноута на комп.

Запрос.
```sql
UPDATE work_rez
SET payment=payment*operation_num*(100-(SELECT medical_staff.tax from medical_staff,work_rez where medical_staff.id=work_rez.worker_id AND work_rez.payment=payment ))/100;
```

Результат.
![image](https://user-images.githubusercontent.com/99073996/201056944-21c794fc-41b0-47c7-9eed-6e6fa5f6e11c.png)


#### Задаение 9.
Тут я очень долго не мог понять, как добавить в таблицу об операциях (для меня это operation_type - таблица с индексом операции, местом проведения и т.д.) информацию об отчислении в бюджет. 

```sql
ALTER TABLE operation_type
ADD tax INT;
UPDATE operation_type
set tax=price*(Select sum(work_rez.operation_num*work_plase.tax) from work_rez, work_plase
               where work_rez.plase_id=work_plase.id
               and work_rez.operation_id=1)/100
WHERE operation_type.id=1;
UPDATE operation_type
set tax=price*(Select sum(work_rez.operation_num*work_plase.tax) from work_rez, work_plase
               where work_rez.plase_id=work_plase.id
               and work_rez.operation_id=2)/100
WHERE operation_type.id=2;
UPDATE operation_type
set tax=price*(Select sum(work_rez.operation_num*work_plase.tax) from work_rez, work_plase
               where work_rez.plase_id=work_plase.id
               and work_rez.operation_id=3)/100
WHERE operation_type.id=3;
UPDATE operation_type
set tax=price*(Select sum(work_rez.operation_num*work_plase.tax) from work_rez, work_plase
               where work_rez.plase_id=work_plase.id
               and work_rez.operation_id=4)/100
WHERE operation_type.id=4;
UPDATE operation_type
set tax=price*(Select sum(work_rez.operation_num*work_plase.tax) from work_rez, work_plase
               where work_rez.plase_id=work_plase.id
               and work_rez.operation_id=5)/100
WHERE operation_type.id=5;
UPDATE operation_type
set tax=price*(Select sum(work_rez.operation_num*work_plase.tax) from work_rez, work_plase
               where work_rez.plase_id=work_plase.id
               and work_rez.operation_id=6)/100
WHERE operation_type.id=6;
UPDATE operation_type
set tax=price*(Select sum(work_rez.operation_num*work_plase.tax) from work_rez, work_plase
               where work_rez.plase_id=work_plase.id
               and work_rez.operation_id=7)/100
WHERE operation_type.id=7;
```

Результат.

![image](https://user-images.githubusercontent.com/99073996/201079232-cf8c8d35-5577-421c-bc69-2ef26c4fba69.png)
