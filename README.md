# Базы данных и SQL (семинары)

## Урок 2. SQL – создание объектов, простые запросы выборки

1. _Используя операторы языка SQL, 
    создайте таблицу “sales”. Заполните ее данными._

    ```
        CREATE database lesson_2;
        use lesson_2;

        CREATE TABLE sales
        (
            id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
            order_date DATE NOT NULL DEFAULT (CURRENT_DATE),
            count_product INT UNSIGNED NOT NULL
        );

        # ---------------  Заполнение таблицы  -----------------------

        INSERT sales (order_date, count_product)
        VALUES
            ( "2022-01-01", 156),
            ( "2022-01-02", 180),
            ( "2022-01-03", 21),
            ( "2022-01-04", 124),
            ( "2022-01-05", 341);

    ```

2.  _Для данных таблицы “sales” укажите тип заказа в зависимости от кол-ва: 
    меньше 100 - Маленький заказ, от 100 до 300 - Средний заказ, больше 300 - Большой заказ_

    ```

    SELECT id AS "id заказа", 
        CASE 
            WHEN count_product < 100 THEN "Маленький заказ"
            WHEN count_product <= 300 THEN "Средний заказ"
            ELSE "Большой заказ"
        END AS "Тип заказа"
    FROM sales;
    ```

