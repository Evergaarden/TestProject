

<center><b><h2>Краткое содержание БД "Компьютерная фирма":</h2></b></center>

Схема БД состоит из четырех таблиц:

1) <b>Product</b> (<b>maker</b>, <b>model</b>, <b>type</b>) Таблица представляет:
<ul type="square"><li><b>maker</b> - производитель,</li> 
  <li><b>model</b> - номер модели,</li>
  <li><b>type</b> - тип ('PC' - ПК, 'Laptop' - ПК-блокнот или 'Printer' - принтер).</li> 
</ul>
2) <b>PC</b> (<b>code</b>, <b>model</b>, <b>speed</b>, <b>ram</b>, <b>hd</b>, <b>cd</b>, <b>price</b>) В таблице PC:
<ul type="square"><li><b>code</b> (для каждого ПК, однозначно определяемого уникальным кодом),</li>
<li><b>model</b> (внешний ключ к таблице Product),</li>
  <li><b>speed</b> - скорость процессора в мегагерцах,</li> 
  <li><b>ram</b> - объем памяти в мегабайтах,</li> 
  <li><b>hd</b> - размер диска в гигабайтах,</li> 
  <li><b>cd</b> - скорость считывающего устройства (например, '4x'),</li>
  <li><b>price</b> - цена</li>
</ul>
3) <b>Laptop<b> (<b>code</b>, <b>model</b>, <b>speed</b>, <b>ram</b>, <b>hd</b>, <b>price</b>, <b>screen</b>) В таблице Laptop:
  <ul type="square"><li><b>code</b> (для каждого ПК, однозначно определяемого уникальным кодом),</li>
    <li><b>model</b> (внешний ключ к таблице Product),</li>
    <li><b>speed</b> - скорость процессора в мегагерцах,</li>
    <li><b>ram</b> - объем памяти в мегабайтах,</li>
    <li><b>hd</b> - размер диска в гигабайтах,</li>
    <li><b>price</b> - цена,</li>
    <li><b>screen</b> - размер экрана в дюймах.</li></ul>

  4) <b>Printer</b> (<b>code</b>, <b>model</b>, <b>color</b>, <b>type</b>, <b>price</b>)  В таблице Printer: 
  <ul type="square"><li><b>code</b> - уникальный код,</li>
    <li><b>model</b> - модель принтера,</li>
    <li><b>color</b> - для каждой модели принтера указывается, является ли он цветным  ('y', если цветной),</li> 
    <li><b>type</b> - тип принтера (лазерный – 'Laser', струйный – 'Jet' или матричный – 'Matrix'),</li>
    <li><b>price</b> - цена.</li></ul>

======================================================================

<br><b>Задание 1:</b>
<br>Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd

        SELECT model, speed, hd
        FROM PC
        WHERE price < 500



====================
<br><b>Задание 2:</b>
<br>Найдите производителей принтеров. Вывести: maker

        SELECT DISTINCT maker
        FROM Product
        WHERE type = 'Printer'


====================
  <br><b>Задание 3:</b>
<br>Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.

        SELECT model, ram, screen 
        FROM Laptop 
        WHERE price > 1000


====================
  <br><b>Задание 4:</b>
<br>Найдите все записи таблицы Printer для цветных принтеров.

        SELECT * 
        FROM Printer
        WHERE color = 'y'


====================
  <br><b>Задание 5:</b>
<br>Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.

        SELECT model, speed, hd
        FROM PC
        WHERE (CD = '12x' OR CD = '24x') AND price < 600


====================
<br><b>Задание 6:</b>
<br>Для каждого производителя, выпускающего ПК-блокноты c объемом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.

        SELECT DISTINCT Product.maker, Laptop.speed
        FROM Product INNER JOIN Laptop ON Product.model = Laptop.model
        WHERE Laptop.hd >= 10 AND Product.type = 'Laptop'


======================
  <br><b>Задание 7:</b>
<br>Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).

        SELECT DISTINCT Product.model, pc.price
        FROM Product INNER JOIN PC ON Product.model = PC.model
        WHERE maker = 'B'
        UNION
        SELECT DISTINCT Product.model, Laptop.price
        FROM Product INNER JOIN Laptop ON Product.model = Laptop.model
        WHERE maker = 'B'
        UNION
        SELECT DISTINCT Product.model, Printer.price
        FROM Product INNER JOIN Printer ON Product.model = Printer.model
        WHERE maker = 'B'

  
======================
  <br><b>Задание 8:</b>
<br>Найдите производителя, выпускающего ПК, но не ПК-блокноты.

        SELECT DISTINCT maker
        FROM Product
        WHERE type = 'pc'
        EXCEPT
        SELECT DISTINCT maker
        FROM Product
        WHERE type = 'laptop'


======================
  <br><b>Задание 9:</b>
<br>Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker

        SELECT DISTINCT Product.maker
        FROM Product INNER JOIN PC ON Product.model = PC.model
        WHERE PC.speed >= 450


======================
  <br><b>Задание 10:</b>
<br>Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price

        SELECT DISTINCT model, price
        FROM Printer 
        WHERE price = (SELECT MAX(price) FROM Printer)


======================
  <br><b>Задание 11:</b>
<br>Найдите среднюю скорость ПК

 
        SELECT AVG(speed)
        FROM PC


======================
  <br><b>Задание 12:</b>
<br>Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.

        SELECT AVG(speed) 
        FROM Laptop
        WHERE price > 1000


======================
  <br><b>Задание 13:</b>
<br>Найдите среднюю скорость ПК, выпущенных производителем A.

        SELECT AVG(PC.speed) AS AVG_speed
        FROM PC INNER JOIN Product ON Product.model = PC.model
        WHERE maker = 'A'



======================
  <br><b>Задание 14:</b>
<br>Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.

        SELECT DISTINCT Ships.class, Ships.name, Classes.country
        FROM Classes INNER JOIN Ships ON Classes.class = Ships.class
        WHERE numGuns >= 10


======================
  <br><b>Задание 15:</b>
<br>Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD

        SELECT HD 
        FROM PC
        GROUP BY HD
        HAVING COUNT(model) >= 2

======================
  <br><b>Задание 19:</b>
<br>Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов. Вывести: maker, средний размер экрана.

        SELECT DISTINCT Product.maker, AVG(screen) AS Avg_screen
        FROM Product INNER JOIN Laptop ON Product.model = Laptop.model
        GROUP BY maker


======================
  <br><b>Задание 20:</b>
<br>Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.

        SELECT maker, COUNT(model) AS Count_Model
        FROM Product
        WHERE type = 'PC'
        GROUP BY maker
        HAVING COUNT(model) >= 3

======================
  <br><b>Задание 21:</b>
<br>Найдите максимальную цену ПК, выпускаемых каждым производителем, у которого есть модели в таблице PC. Вывести: maker, максимальная цена.

        SELECT DISTINCT Product.maker, MAX(price) AS Max_price
        FROM Product INNER JOIN PC ON Product.model = PC.model
        GROUP BY maker


======================
  <br><b>Задание 22:</b>
<br>Для каждого значения скорости ПК, превышающего 600 МГц, определите среднюю цену ПК с такой же скоростью. Вывести: speed, средняя цена.
  
        SELECT speed, AVG(price) AS Avg_price
        FROM PC 
        WHERE speed > 600
        GROUP BY speed


======================
  <br><b>Задание 23:</b>
<br>Найдите производителей, которые производили бы как ПК со скоростью не менее 750 МГц, так и ПК-блокноты со скоростью не менее 750 МГц. Вывести: Maker

        SELECT Product.maker 
        FROM Product INNER JOIN PC ON Product.model = PC.model
        WHERE type = 'PC' AND speed >= 750
        INTERSECT
        SELECT Product.maker 
        FROM Product INNER JOIN Laptop ON Product.model = Laptop.model
        WHERE type = 'Laptop' AND speed >= 750


======================
  <br><b>Задание 24:</b>
<br>Перечислите номера моделей любых типов, имеющих самую высокую цену по всей имеющейся в базе данных продукции.

        WITH Max_price AS
        (SELECT model, MAX(price) AS price_1
        FROM PC
        GROUP BY model
        UNION
        SELECT model, MAX(price) as price_1
        FROM Laptop
        GROUP BY model
        UNION
        SELECT model, MAX(price) as price_1
        FROM Printer
        GROUP BY model)
        SELECT model 
        FROM Max_price
        WHERE price_1 = (SELECT MAX(price_1) FROM Max_price)






















