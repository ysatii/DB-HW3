# Домашнее задание к занятию «SQL. Часть 1» - Мельник Юрий Александрович

## База данных Sakila содержит 16 основных таблиц, описывающих различные аспекты компании по прокату DVD-дисков. Ниже приведен список этих таблиц:

   - actor – информация об актерах, которые участвовали в фильмах.
   - address – информация об адресах, в которых зарегистрированы клиенты компании.
   - category – список категорий, к которым могут относиться фильмы.
   - city – информация о городах, в которых расположены адреса клиентов.
   - country – информация о странах, в которых расположены города.
   - customer – информация о клиентах, которые берут в аренду фильмы.
   - film – информация о фильмах, доступных для проката.
   - film_actor – связь между фильмами и актерами, которые участвуют в этих фильмах.
   - film_category – связь между фильмами и категориями, к которым они относятся.
   - film_text – полный текст сюжетов фильмов, доступных для проката.
   - inventory – информация о DVD-дисках, доступных для проката.
   - language – список языков, на которых доступны фильмы.
   - payment – информация о платежах, сделанных клиентами за аренду фильмов.
   - rental – информация о факте аренды фильма клиентом.
   - staff – информация о сотрудниках компании, работающих в магазине.
   - store – информация о магазинах компании по прокату DVD-дисков.
## Задание 1
Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

## Решение 1  
  нам понадобиться таблица address.   
  Поле **district** - округ!условие LIKE 'K%a' - выберет все округа начинающиеся на **K** оканчивающиеся на **a**
условие  district NOT LIKE '% %' - выберет все кто не имеет пробела внутри, т.е. название района не состоит из двух слов.

запрос имеет вид  
```
SELECT district FROM address WHERE district LIKE 'K%a' AND district NOT LIKE '% %';
```
 ![alt text](https://github.com/ysatii/DB-HW3/blob/main/img/image1.jpg)

для получения уникальных значений нужно добавить DISTINCT в запрос  
```
SELECT DISTINCT district FROM address WHERE district LIKE 'K%a' AND district NOT LIKE '% %';
```
 ![alt text](https://github.com/ysatii/DB-HW3/blob/main/img/image1_1.jpg)

## Задание 2
Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

## Решение 2
Нам понадобиться таблица  **payment**. поле **payment_date** -  дата платежа, **amount** -  сумма платежа  
первый вариант получим все столбцы таблицы в указанном временном промежутке с суммой оплаты боле 10 условных едениц  
```
SELECT * FROM payment WHERE payment_date BETWEEN '2005-06-15 00:00:00' AND '2005-06-18 23:59:59' AND amount > 10;
```
 ![alt text](https://github.com/ysatii/DB-HW3/blob/main/img/image2.jpg)

Второй вариант получим , ид платежа, сумму и дату в формате DATE  
```
SELECT payment_id, amount, CAST(payment_date AS DATE) FROM payment WHERE payment_date BETWEEN '2005-06-15 00:00:00' AND '2005-06-18 23:59:59' AND amount > 10;
```
 ![alt text](https://github.com/ysatii/DB-HW3/blob/main/img/image2_1.jpg)
для отдела бухгалтерии точное время не принципиально!  

## Задание 3
Получите последние пять аренд фильмов.

## Решение 3
Нам понадобиться таблица **rental** поле **return_date**  
Вариант 1  
 выберем все поля послед  TOP 5  
```
SELECT * FROM rental ORDER BY rental_id desc LIMIT 5;
```
 ![alt text](https://github.com/ysatii/DB-HW3/blob/main/img/image3.jpg)

Вариант 2  
узнаем названия популярных фильмой и приведем все поля DATETIME к DATE,
 выведем название и описание фильмой, такая информация будет более полезна для статистики  
 ```
SELECT rental_id, cast(rental_date AS DATE) as rental_date, cast(return_date AS DATE) AS return_date, rental.inventory_id , f.title, f.description FROM rental 
JOIN inventory i ON i.inventory_id = rental.inventory_id 
join film f on f.film_id = i.film_id
ORDER BY rental_id  desc LIMIT 5;
```
 ![alt text](https://github.com/ysatii/DB-HW3/blob/main/img/image3_1.jpg)


можем перепроверить информацию выведенную запросом
inventory информация о DVD-дисках, доступных для проката.
определим id всем фильмов
```
select * from inventory where inventory_id in (2666, 2019, 2088, 4364, 772)
```
 ![alt text](https://github.com/ysatii/DB-HW3/blob/main/img/image3_2.jpg)


film – информация о фильмах, доступных для проката.
получим информацию о фильмах согласно их ид
```
select * from film where film_id in (168,439,452,585,951)
```
 ![alt text](https://github.com/ysatii/DB-HW3/blob/main/img/image3_3.jpg)

## Задание 4
Одним запросом получите активных покупателей, имена которых **Kelly** или **Willie**.

Сформируйте вывод в результат таким образом:

   - все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
   - замените буквы 'll' в именах на 'pp'.

## Решение 4
Нам понадобиться таблица **customer** поля **first_name** - имя и **last_name** - фамилия  
получим всех нужных пользователей  
```
SELECT first_name AS Имя, last_name AS Фамилия FROM customer
WHERE active = 1 AND (first_name LIKE 'Kelly' OR first_name LIKE 'Willie');
```
 ![alt text](https://github.com/ysatii/DB-HW3/blob/main/img/image4.jpg)

применим все условия задания
```
SELECT LOWER(REPLACE(first_name, 'LL', 'PP')) AS Имя, LOWER(last_name) AS Фамилия FROM customer
WHERE active = 1 AND (first_name LIKE 'Kelly' OR first_name LIKE 'Willie');
```
 ![alt text](https://github.com/ysatii/DB-HW3/blob/main/img/image4_1.jpg)

## Задание 5*

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

## Решение 5


## Задание 6* 

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

## Решение 6
