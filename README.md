# Базы данных и SQL (семинары)

## Урок 1. Установка СУБД, подключение к БД, просмотр и создание таблиц

1. Создайте таблицу с мобильными телефонами, используя графический интерфейс. Заполните БД данными.

   <img src= "phones_table.png" alt="Таблица phones" style="width:700px;"/>
   
2. Выведите название, производителя и цену для товаров, количество которых превышает 2

```
use lesson1;

select ProductName, Manufacturer, Price
from phones
where ProductCount > 2;
```
<img src= "product_count_gt2.png" alt="products with count > 2" style="width:700px;"/>

3. Выведите весь ассортимент товаров марки "Samsung"

```
use lesson1;

select ProductName from phones
where Manufacturer = 'Samsung';
```
<img src= "samsung.png" alt="samsung products" style="width:700px;"/>

4.  С помощью регулярных выражений найти (можно использовать операторы “LIKE”, “RLIKE”):
    - Товары, в которых есть упоминание "Iphone"
        ```
        use lesson1;

        select ProductName, Manufacturer, ProductCount, Price from phones
        where ProductName LIKE '%iPhone%'; 
        ```
    <img src= "iPhones.png" alt="iPhones" style="width:700px;"/>
    
    - "Galaxy"
        ```
        use lesson1;

        select ProductName, Manufacturer, ProductCount, Price from phones
        where ProductName LIKE '%Galaxy%'; 
        ```
    <img src= "galaxy.png" alt="Galaxy" style="width:700px"/>

    - Товары, в которых есть ЦИФРЫ

        ```
        use lesson1;

        select ProductName, Manufacturer, ProductCount, Price from phones
        where ProductName rlike '\\d';
        ```
        <img src= "with_digits.png" alt="phones with digits" style="width:700px"/>

    - Товары, в которых есть ЦИФРА "8"

        ```
        use lesson1;

        select ProductName, Manufacturer, ProductCount, Price from phones
        where ProductName rlike '8';
        ```
        или

        ```
        use lesson1;

        select ProductName, Manufacturer, ProductCount, Price from phones
        where ProductName like '%8%';
        ```

         <img src= "only8.png" alt="phones with digit 8" style="width:700px"/>