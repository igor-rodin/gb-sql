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

        INSERT sales(order_date, count_product)
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
    use lesson_2;

    SELECT id AS "id заказа", 
        CASE 
            WHEN count_product < 100 THEN "Маленький заказ"
            WHEN count_product <= 300 THEN "Средний заказ"
            ELSE "Большой заказ"
        END AS "Тип заказа"
    FROM sales;
    ```
3. Создайте таблицу “orders”, заполните ее значениями. Выберите все заказы. В зависимости от поля order_status выведите столбец full_order_status:
    OPEN – «Order is in open state»; CLOSED - «Order is closed»; CANCELLED -  «Order is cancelled»


    ```
    use lesson_2;

    CREATE TABLE orders
    (
        id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
        employee_id varchar(10) NOT NULL,
        amount float(10,2) NOT NULL,
        order_status ENUM("OPEN", "CLOSED", "CANCELLED") NOT NULL DEFAULT ('OPEN')
    );

    # ---------------  Заполнение таблицы  -----------------------

    INSERT orders(employee_id, amount, order_status)
    VALUES
        ( "e03", 15.00, "OPEN"),
        ( "e01", 25.50, "OPEN"),
        ( "e05", 100.70, "CLOSED"),
        ( "e02", 22.18, "OPEN"),
        ( "e04", 9.50, "CANCELLED");

    # ---------------  Выборка -----------------------

    SELECT id AS order_id, 
        CASE order_status
            WHEN "OPEN" THEN "Order is in open state"
            WHEN "CLOSED" THEN "Order is closed"
            ELSE "Order is cancelled"
        END AS full_order_status
    FROM orders;

    ```
