
# Итоговая aттecтaция

Необходимо организовать систему учета для питомника, в котором живут домашние и вьючные животные.

### Задание (Linux)

1. Используя команду ``cat`` в терминале операционной системы Linux, создать два файла:   `Домашние животные` (заполнив файл `собаками, кошками, хомяками`) `Вьючные животные` (заполнив файл `лошадьми, верблюдами, ослами`), а затем объединить их. Просмотреть содержимое созданного файла. Переименовать файл, дав ему новое имя - `Друзья человека`.
2. Создать директорию, переместить файл туда.
3. Подключить дополнительный репозиторий MySQL. Установить любой пакет из этого репозитория.
4. Установить и удалить deb-пакет с помощью ``dpkg``.
5. Выложить историю команд в терминале Ubuntu.  

### Задание (SQL)
6. Нарисовать диаграмму, в которой есть класс родительский класс, домашние животные и вьючные животные, в составы которых в случае `домашних животных` войдут классы: `собаки`, `кошки` и `хомяки`, а в класс `вьючные животные` войдут: `лошади`, `верблюды` и `ослы`. 
7. В подключенном MySQL репозитории создать базу данных `Друзья человека`.
8. Создать таблицы с иерархией из диаграммы в БД.
9. Заполнить низкоуровневые таблицы именами животных, командами, которые они выполняют и датами рождения.
10. Объединить таблицы `лошади` и `ослы` в одну таблицу, удалив из таблицы `верблюдов`, так как верблюдов решили перевезти в другой питомник на зимовку.  
11. Создать новую таблицу `молодые животные` в которую попадут все животные старше 1 года, но младше 3 лет и в отдельном столбце с точностью до месяца подсчитать возраст животных в новой таблице.
12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на прошлую принадлежность к старым таблицам  

### 3. Задание (Java)
13. Создать класс с инкапсуляцией методов и наследованием по диаграмме.
14. Написать программу, имитирующую работу реестра домашних животных. В программе должен быть реализован следующий функционал:  
- 1. Заводить новое животное  
- 2. Определять животное в правильный класс
- 3. Увидеть список команд, которое выполняет животное
- 4. Обучить животное новым командам
- 5. Реализовать навигацию по меню*  

15. Создайте класс `Счетчик`, у которого есть метод ``add()``, увеличивающий значение внутренней ``int`` переменной на `1` при нажатии `Завести новое животное`. Сделайте так, чтобы с объектом такого типа можно было работать в блоке ``try-with-resources``. Нужно бросить исключение, если работа с объектом типа счетчик была не в ресурсном ``try`` и/или ресурс остался открыт. Значение считать в ресурсе ``try``, если при заведении животного заполнены все поля.  


## Решение

### Пункт 1
Создаем файл `Домашние_животные` и заполняем его данными (животное кличка возраст(месацы))

```bash
$ cat > Домашние_животные
cобака Бим 25
кошка Мурка 19
хомяк Чип 12
```

Создаем файл `Вьючные_животные` и заполняем его данными (животное кличка возраст(месацы))

```bash
$ cat > Вьючные_животные
лошадь Атива 48
верблюд Сахара 100
осел Иа 36
```

Объединяем файлы `Домашние_животные` и `Вьючные_животные`:

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


### Пункт 2
Создаем директорию `Животные`:

```bash
$ mkdir Животные
```

Перемещаем файл `Друзья_человека` в директорию `Животные`:

```bash
$ mv Друзья_человека Животные/
```

### Пункт 3
Подключаем дополнительный репозиторий `MySQL`. Устанавливаем любой пакет из этого репозитория:

```bash
$ sudo wget https://dev.mysql.com/get/mysql-apt-config_0.8.24-1_all.deb
$ sudo dpkg -i mysql-apt-config_0.8.24-1_all.deb
$ sudo apt update
$ sudo apt install mysql-server mysql-client
$ systemctl status mysql.service
```

### Пункт 4
Устанавливаем и удаляем `deb-пакет` с помощью `dpkg`:

```bash
$ sudo dpkg -i mysql-apt-config_0.8.24-1_all.deb
$ sudo dpkg -r mysql-apt-config
$ sudo dpkg --purge mysql-apt-config
```

### Пункт 7
Cоздаем базу данных `Друзья человека`:

```sql
CREATE DATABASE IF NOT EXISTS HumanFriends;
USE HumanFriends;
```

### Пункт 8
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

### Пункт 9
Заполняем низкоуровневые таблицы `именами животных`, `командами`, `датами рождения`

```sql
USE HumanFriends;

INSERT INTO Commands(name)
VALUES
 ('Кушать'),
 ('Играть'),
 ('Сидеть'),
 ('Стоять'),
 ('Лежать');
  
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
 ('Бим', '2018-07-01', 1),
 ('Мурка', '2017-09-01', 2),
 ('Чип', '2022-07-01', 3),
 ('Атива', '2017-09-01', 4),
 ('Сахара', '2016-12-01', 5),
 ('Иа', '2017-04-01', 6);
   
INSERT INTO AnimalCommands (animal_id, command_id)
VALUES
 (1, 1), (1, 2), (2, 3), (3, 5),
 (4, 1), (4, 4), (5, 5), (6, 4),
 (6, 5);
```

### Пункт 10
Объединяем таблицы `лошади` и `ослы` в одну таблицу, удалив из таблицы `верблюдов`

```sql
USE HumanFriends;
DELETE FROM KennelAnimal WHERE genius_id = 5;

CREATE TABLE HorseAndDonkey AS
SELECT * from KennelAnimal WHERE genius_id = 4
UNION
SELECT * from KennelAnimal WHERE genius_id = 6;
```

### Пункт 11
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

### Пункт 12
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