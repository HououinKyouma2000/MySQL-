# MySQL-
Изучение MySQL команд

команда запуска mysql -u root -p
потом пароль: ____


показ дат баз которые имеются SHOW DATABASE;  
создание базы  CREATE DATABASE _____;  Название
удаление DROP DATABASE _____; 
для действий над базами либо выбора пишется скрипт  USE _____;
Чтоб посмотреть на таблицы внутри базы show tables;
Чтоб создать таблицу CREATE TABLE ____(     название таблицы открываем скобку  чтоб дальше вводить поля 


В нашем случае это таблица будет teacher а поля id или колонки 


id INT AUTO_INCREMENT PRIMARY KEY,

В начале создаем уникальный идентификатор id 
Которое будет числого значения INT 
Он будет  AUTO_INCREMET то есть каждая следующая запись на +1 предыдущего
Так же указали что это первичный ключ  PRIMARY KEY
Запятая так как мы перечисляем 

 
surname VARCHAR(255) NOT NULL

Второе поле фамилия учителя surname
оно строковое значит VARCHAR 
Оно не может быть пустыс NOT NULL
здесь без запятой так как это последеяя


); 

закрываем скобку


потом можно show tables; чтоб посмотреть 

show columns FROM teacher;

покажет внутринности таблици 


CREATE TABLE lesson(
    -> id INT AUTO_INCREMENT PRIMARY KEY,
    -> name VARCHAR(255) NOT NULL,
    -> teacher_id INT NOT NULL,
    -> FOREIGN KEY (teacher_id) references teacher(id)
    -> );

создаем таблицу уроков и тут важно то что у нас есть поле учитель АЙДИ
и по сути это поле берется из предыдущей таблици поэтому указываем внешеию
связь поля (teacher_id) с полем teacher(id) то есть поле id из таблицы teacher
Тут тип связи один ко многим и указываем что поле teacher_id имеет внешникй ключ


INSERT INTO teacher (surname) values ("Иванов");
INSERT INTO teacher (surname) values ("Петров");

Мы вводим значения в поля через скрипт INSERT INTO название таблици 
потом в скобках название поля потом слово values и значение в скобках

SELECT * FROM teacher;

означает показать все * значения таблици teacher

SELECT id FROM teacher;
 
дает лишь колонку id

SELECT surname FROM teacher;

колонка surname

SELECT surname,id,surname FROM teacher;

можно перечислять через запятую и повторять тогда мы получим таблицу где колонки повторяются

SELECT DISTINCT surname FROM teacher;

DISTINCT означает уникальные значения


SELECT * FROM teacher WHERE id>8;
SELECT * FROM teacher WHERE id=7;
SELECT * FROM teacher WHERE surname="Petrov";


это означает что он будет выводить по условию


SELECT * FROM teacher WHERE surname="Petrov" LIMIT 2;

из-за того что у нас Петровых 3 мы можем создать лимит вывода только двух петровых

SELECT * FROM teacher LIMIT 4;

означает просто вывод 4 первых полей 


SELECT id AS 'Identifikator' , surname AS 'Familiya' FROM teacher;

это строка просто меняет вид вывода то есть вместо слов  id в колонке будет  Identifikator
но в следующий раз при вызове простого вывода все будет стандарто с id 


SELECT * FROM teacher ORDER BY surname;

сортирует данные по имени

SELECT * FROM teacher ORDER BY surname DESK;

означает обратный порядок 


ALTER TABLE teacher ADD age INT;

это значит что в таблицу teacher мы добавляем колону age типа INT 


UPDATE teacher SET age = 20 WHERE id =1;

устанавливаем значения поля age по соответсвующим id

UPDATE teacher SET age = 20; 

при тако записи значения меняются у всех

SELECT * FROM teacher WHERE surname LIKE "%ov";

означает что будут выведены поля где есть ov


SELECT * FROM teacher WHERE id > 10 AND age <45;
OR тоже можно
NOT
означает логическое условие по двум 


SELECT * FROM teacher WHERE age BETWEEN 35 and 45;

означает между этими двумя значениями


DELETE FROM teacher WHERE id =12;

удаление поля 

DELETE FROM teacher;

удаление всех полей


INSERT INTO lesson (name, teacher_id) values ("Matematika",7), ("Informatika",7), ("Russkiy",8), ("Fizika",9);

добавления данных через запятую 


Теперь нужно понять важную вещь ведь наши две таблици в какойто мере несут общий смысл . Одна просто перечесление учителей а другая уроков где так же есть айди учителя
По сути мы можем их соединить но ведь некоторые учителя не ведут уроков а некоторых предметов нет и тд много нюансов 
Это схема Эллера с двумя множествами и нужно выбрать что тут мы оставим 
либо пересечение двух таблиц то есть  A AND B так называемое внутреннее объядинение iner join

Или есть внешенее OUTER JOIN где по сути происходит операция 
(NOT B) OR (A AND B)=A По сути тут получается мы вводим все значения учителей если даже они не ведут уроки
или (NOT A) OR  (A AND B)=B Тут обратно , по сути это таблица уроков среди которых могут быть те которые не имеют учителя

FULL JOIN  куда входят все A or B хотя пересечение наверное один раз


SELECT teacher.surname , lesson.name FROM teacher INNER JOIN lesson ON teacher.id = lesson.teacher_id;

Чтоб получить новую таблицу указываем чере запятую колоники  написав название таблици точка название колонки
Тут мы делаем внешне левое слияние поэтому после FROM пишем таблицу teacher
потом INNER JOIN и таблицу правую lesson 
потом ключевое слово ON
потом столбци по которым будет объядинение то есть столбци которые мы связали teacher.id=lesson.teacher_id


SELECT teacher.surname , lesson.name FROM teacher LEFT OUTER JOIN lesson ON teacher.id = lesson.teacher_id;

это внешне левое обЪядинение


SELECT teacher.surname , lesson.name FROM teacher RIGHT OUTER JOIN lesson ON teacher.id = lesson.teacher_id;

правое

SELECT * FROM teacher UNION SELECT * FROM lesson;

это уже простое объядинение по вертикали


SELECT AVG(age) FROM teacher;

вычисляет ср арифметическое всей колонки age


SELECT MAX(age) FROM teacher;
SELECT MIN(age) FROM teacher;
SELECT SUM(age) FROM teacher;



SELECT age,COUNT(age) FROM teacher GROUP BY age;

выводит таблицу где показано сколько одинаковых значений по колонке age имеется
