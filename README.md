# Базы данных и SQL (семинары)

## Урок 4. SQL – работа с несколькими таблицами

### *Используя JOIN-ы, выполните следующие операции:*

1. Вывести всех котиков по магазинам по id (условие соединения shops.id = cats.shops_id)

    ``` sql
        use lesson_4;

        SELECT c.`name`, sh.shopname
        FROM cats c
        INNER JOIN shops sh
        ON c.shops_id = sh.id;
    ```

2. Вывести магазин, в котором продается кот “Мурзик”

    ``` sql
        use lesson_4;
        -- a) через подзапрос
        SELECT sh.shopname, t.`name`
        FROM shops sh
        INNER JOIN
            (
                SELECT `name`, shops_id FROM cats
                WHERE `name` = 'Murzik'
            ) t
        ON sh.id = t.shops_id

        --b)
        SELECT sh.shopname, c.`name`
        FROM shops sh
        INNER JOIN cats c
        ON c.shops_id = sh.id
        WHERE c.`name` = 'Murzik'
    ```

### *Вывести название и цену для всех анализов, которые продавались 5 февраля 2020 и всю следующую неделю.*

```sql
        use lesson_4;
        -- Запрос написан в предположении, что дата "5 февраля 2020" входит в неделю.
        -- Если подрузамевалось, что нужный диапазон дней это "5 февраля 2020" и плюс неделя,
        -- то в запросе надо "INTERVAL 7 DAY" заменить на "INTERVAL 8 DAY".

        -- a)
        SELECT a.an_name, a.an_price, o.ord_datetime
        FROM Analysis a
        INNER JOIN Orders o
        ON an_id = o.ord_an
        WHERE o.ord_datetime BETWEEN '2020-02-05' AND '2020-02-05' + INTERVAL 7 DAY
        ORDER BY o.ord_datetime DESC;

        --b) с помощью подзапроса
        SELECT a.an_name, a.an_price, t.ord_datetime
        FROM Analysis a
        INNER JOIN
            (
                SELECT ord_datetime, ord_an
                FROM Orders WHERE ord_datetime BETWEEN '2020-02-05' AND '2020-02-05' + INTERVAL 7 DAY
            ) t
        ON a.an_id = t.ord_an
        ORDER BY t.ord_datetime DESC;
```
