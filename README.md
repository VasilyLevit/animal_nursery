
# Итоговая aттecтaция

## Зaдaниe

Необходимо организовать систему учета для питомника, в котором живут домашние и вьючные животные.

### 1. Задание на проверку навыков работы в операционной системе Linux Ubuntu

1.1. Используя команду `cat` в терминале операционной системы `Linux`, создать два файла:
  - `Домашние животные` (заполнив файл `собаками`, `кошками`, `хомяками`)
  - `Вьючные животные` (заполнив файл `лошадьми`, `верблюдами`, `ослами`)

Затем объединить их. Просмотреть содержимое созданного файла. Переименовать файл, дав ему новое имя - `Друзья человека`.

1.2. Создать директорию, переместить файл туда  
1.3. Подключить дополнительный репозиторий `MySQL`. Установить любой пакет из этого репозитория  
1.4. Установить и удалить `deb-пакет` с помощью `dpkg`  
1.5. Выложить историю команд в терминале `Ubuntu`  

### 2. Задание на проверку навыков работы c MySQL

2.1. Нарисовать диаграмму, в которой есть класс родительский класс, домашние животные и вьючные животные, в составы которых в случае `домашних животных` войдут классы: `собаки`, `кошки` и `хомяки`, а в класс `вьючные животные` войдут: `лошади`, `верблюды` и `ослы`  
2.2. В подключенном `MySQL` репозитории создать базу данных `Друзья человека`  
2.3. Создать таблицы с иерархией из диаграммы в БД  
2.4. Заполнить низкоуровневые таблицы `именами животных`, `командами` которые они выполняют и `датами рождения`  
2.5. Объединить таблицы `лошади` и `ослы` в одну таблицу, удалив из таблицы `верблюдов`, так как верблюдов решили перевезти в другой питомник на зимовку  
2.6. Создать новую таблицу `молодые животные` в которую попадут все животные старше `1` года, но младше `3` лет и в отдельном столбце с точностью до месяца подсчитать возраст животных в новой таблице  
2.7. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на прошлую принадлежность к старым таблицам  

### 3. Задание на использование языка Java

3.1. Создать класс с __инкапсуляцией__ методов и наследованием по диаграмме  
3.2. Написать программу, имитирующую работу реестра домашних животных  
3.3. В программе должен быть реализован следующий функционал:  
&#8203; &#8203; &#8203; &#8203; &#8203; &#8203;3.3.1. *Заводить новое животное*  
&#8203; &#8203; &#8203; &#8203; &#8203; &#8203;3.3.2. *Определять животное в правильный класс*  
&#8203; &#8203; &#8203; &#8203; &#8203; &#8203;3.3.3. *Увидеть список команд, которое выполняет животное*  
&#8203; &#8203; &#8203; &#8203; &#8203; &#8203;3.3.4. *Обучить животное новым командам*  
&#8203; &#8203; &#8203; &#8203; &#8203; &#8203;3.3.5. *Реализовать навигацию по меню*  
3.4. Создайте класс `Счетчик`, у которого есть метод `add()`, увеличивающий начение внутренней `int` переменной на `1` при нажатии `Завести новое животное`. Сделайте так, чтобы с объектом такого типа можно было работать в блоке `try-with-resources`. Нужно бросить исключение, если работа с объектом типа счетчик была не в ресурсном `try` и/или ресурс остался открыт. Значение считать в ресурсе `try`, если при заведении животного заполнены все поля  


## Решение

### 1. Задание на проверку навыков работы в операционной системе Linux Ubuntu

<details>
<summary><b>1.1.</b></summary>

Создаем файл `Домашние_животные` и вводим в него данные с клавиатуры:

```bash
$ cat > Домашние_животные
# Домашнее животное Кличка Возраст в месяцах
cобака Дог 25
кошка Кэт 19
хомяк Хамстер 12
```

Создаем файл `Вьючные_животные` и вводим в него данные с клавиатуры:

```bash
$ cat > Вьючные_животные
# Вьючное животное Кличка Возраст в месяцах
лошадь Хорс 48
верблюд Кэмел 100
осел Данки 36
```

Объединяем созданные файлы `Домашние_животные` и `Вьючные_животные`:

```bash
$ cat Домашние_животные Вьючные_животные > Все_животные
```

Просматриваем содержимое созданного файла `Все_животные`:

```bash
$ cat Все_животные
```

Переименовываем файл `Все_животные` в `Друзья_человека`:

```bash
$ mv Все_животные Друзья_человека
```

![](./images/1.1.Screenshot.png "Задание 1.1.")

</details>

<details>
<summary><b>1.2.</b></summary>

Создаем директорию `Животные`:

```bash
$ mkdir Животные
```

Перемещаем файл `Друзья_человека` в директорию `Животные`:

```bash
$ mv Друзья_человека Животные/
```

![](./images/1.2.Screenshot.png "Задание 1.2.")

</details>

<details>
<summary><b>1.3.</b></summary>

Подключаем дополнительный репозиторий `MySQL`. Устанавливаем любой пакет из этого репозитория:

```bash
$ sudo wget https://dev.mysql.com/get/mysql-apt-config_0.8.24-1_all.deb
$ sudo dpkg -i mysql-apt-config_0.8.24-1_all.deb
$ sudo apt update
$ sudo apt install mysql-server mysql-client
$ systemctl status mysql.service
```

![](./images/1.3.1.Screenshot.png "Задание 1.3.")
![](./images/1.3.2.Screenshot.png "Задание 1.3.")

</details>

<details>
<summary><b>1.4.</b></summary>

Устанавливаем и удаляем `deb-пакет` с помощью `dpkg`:

```bash
$ sudo dpkg -i mysql-apt-config_0.8.24-1_all.deb
$ sudo dpkg -r mysql-apt-config
$ sudo dpkg --purge mysql-apt-config
```

![](./images/1.4.Screenshot.png "Задание 1.4.")

</details>

<details>
<summary><b>1.5.</b></summary>

История команд для заданий с 1.1. по 1.4.:

![](./images/1.5.Screenshot.png "Задание 1.5.")

</details>

### 2. Задание на проверку навыков работы c MySQL

<details>
<summary><b>2.1.</b></summary>

Диаграмма классов:

![](./images/uml.drawio.png "Диаграмма классов")
 
</details>

<details>
<summary><b>2.2.</b></summary>

Cоздаем базу данных `Друзья человека`:

```sql
CREATE DATABASE IF NOT EXISTS HumanFriends;
USE HumanFriends;
```

![](./images/2.2.Screenshot.png "Задание 2.2.")

</details>

<details>
<summary><b>2.3.</b></summary>

Создаем таблицы с иерархией из диаграммы в БД:

```sql
CREATE TABLE Commands
(
    id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    name varchar(30),
    description varchar(255)
);

CREATE TABLE AnimalGroup
(
    id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    name varchar(30)
);
   
CREATE TABLE AnimalGenius
(
    id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    name varchar(30),
    group_id INT,
    FOREIGN KEY (group_id) REFERENCES AnimalGroup (id)
    ON DELETE CASCADE ON UPDATE CASCADE
);
   
CREATE TABLE KennelAnimal
(
    id INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    name varchar(30),
    birthDate DATE, 
    genius_id INT,
    FOREIGN KEY (genius_id) REFERENCES AnimalGenius (id)
    ON DELETE CASCADE ON UPDATE CASCADE
);
   
CREATE TABLE AnimalCommands
(
    animal_id INT NOT NULL,
    command_id INT NOT NULL,

    PRIMARY KEY (animal_id, command_id),
    FOREIGN KEY (animal_id) REFERENCES KennelAnimal (id)
     ON DELETE CASCADE ON UPDATE CASCADE,
    FOREIGN KEY (command_id) REFERENCES Commands (id)
     ON DELETE CASCADE  ON UPDATE CASCADE
);
```

![](./images/2.3.Screenshot.png "Задание 2.3.")

</details>

<details>
<summary><b>2.4.</b></summary>

Заполняем низкоуровневые таблицы `именами животных`, `командами` которые они выполняют и `датами рождения`:

```sql
USE HumanFriends;

INSERT INTO Commands(name)
VALUES
 ('Ко мне'),
 ('Аппорт'),
 ('Сидеть'),
 ('Стоять'),
 ('Назад');
  
INSERT INTO AnimalGroup (name)
VALUES
 ('Домашние животные'),
 ('Вьючные животные');
  
INSERT INTO AnimalGenius (name, group_id)
VALUES
 ('Собака', 1),
 ('Кошка', 1),
 ('Хомяк', 1),
 ('Лошадь', 2),
 ('Верблюд', 2),
 ('Осел', 2);
   
INSERT INTO KennelAnimal (name, birthDate, genius_id)
VALUES
 ('Дог', '2020-03-08', 1),
 ('Кэт', '2018-09-10', 2),
 ('Хамстер', '2022-07-15', 3),
 ('Хорс', '2020-09-05', 4),
 ('Кэмел', '2019-12-10', 5),
 ('Данки', '2017-04-08', 6);
   
INSERT INTO AnimalCommands (animal_id, command_id)
VALUES
 (1, 1), (1, 2), (2, 3), (3, 5),
 (4, 1), (4, 4), (5, 5), (6, 4),
 (6, 5);
```

![](./images/2.4.1.Screenshot.png "Задание 2.4.")
![](./images/2.4.2.Screenshot.png "Задание 2.4.")
![](./images/2.4.3.Screenshot.png "Задание 2.4.")
![](./images/2.4.4.Screenshot.png "Задание 2.4.")
![](./images/2.4.5.Screenshot.png "Задание 2.4.")

</details>

<details>
<summary><b>2.5.</b></summary>

Объединяем таблицы `лошади` и `ослы` в одну таблицу, удалив из таблицы `верблюдов`, так как верблюдов решили перевезти в другой питомник на зимовку:

```sql
USE HumanFriends;
DELETE FROM KennelAnimal WHERE genius_id = 5;

CREATE TABLE HorseAndDonkey AS
SELECT * from KennelAnimal WHERE genius_id = 4
UNION
SELECT * from KennelAnimal WHERE genius_id = 6;
```

![](./images/2.5.1.Screenshot.png "Задание 2.5.")
![](./images/2.5.2.Screenshot.png "Задание 2.5.")

</details>

<details>
<summary><b>2.6.</b></summary>

Создаем новую таблицу `молодые животные` в которую попадут все животные старше `1` года, но младше `3` лет. В отдельном столбце в новой таблице подсчитываем возраст животных с точностью до месяца:

```sql
USE HumanFriends;
CREATE TABLE YoungAnimals AS
SELECT id, name, birthDate, 
datediff(curdate(),birthDate) DIV 31 as age, genius_id 
from KennelAnimal 
WHERE date_add(birthDate, INTERVAL 1 YEAR) < curdate() 
AND date_add(birthDate, INTERVAL 3 YEAR) > curdate();
```

![](./images/2.6.Screenshot.png "Задание 2.6.")

</details>

<details>
<summary><b>2.7.</b></summary>

Объединяем все таблицы в одну, при этом сохраняя поля, указывающие на прошлую принадлежность к старым таблицам:

```sql
USE HumanFriends;
CREATE TABLE CombinedAnimals
(
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(30),
    birthDate DATE,
    age INT,
    genius_id INT,
    source_table VARCHAR(30)
);
```

```sql
INSERT INTO CombinedAnimals (name, birthDate, age, genius_id, source_table)
SELECT name, birthDate, age, genius_id, 'YoungAnimals' FROM YoungAnimals;

INSERT INTO CombinedAnimals (name, birthDate, age, genius_id, source_table)
SELECT name, birthDate, NULL, genius_id, 'AnimalGenius' FROM AnimalGenius;

INSERT INTO CombinedAnimals (name, birthDate, age, genius_id, source_table)
SELECT name, NULL, NULL, id, 'AnimalGroup' FROM AnimalGroup;

INSERT INTO CombinedAnimals (name, birthDate, age, genius_id, source_table)
SELECT name, NULL, NULL, id, 'Commands' FROM Commands;

INSERT INTO CombinedAnimals (name, birthDate, age, genius_id, source_table)
SELECT name, birthDate, NULL, genius_id, 'HorseAndDonkey' FROM HorseAndDonkey;

INSERT INTO CombinedAnimals (name, birthDate, age, genius_id, source_table)
SELECT name, birthDate, NULL, genius_id, 'KennelAnimal' FROM KennelAnimal;
```

![](./images/2.7.Screenshot.png "Задание 2.7.")

</details>

### 3. Задание на использование языка Java

Проект представлен в папке Java
