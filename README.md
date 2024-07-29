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
SELECT DISTINCT district FROM address WHERE district LIKE 'K%a' AND district NOT LIKE '% %';
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


## Задание 3
Получите последние пять аренд фильмов.

## Решение 3

## Задание 4
Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:

   - все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
   - замените буквы 'll' в именах на 'pp'.

## Решение 4

## Задание 5*

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

## Решение 5

## Задание 6* 

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

## Решение 6
