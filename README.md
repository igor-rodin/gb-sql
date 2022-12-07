# Базы данных и SQL (семинары)

## Урок 6. SQL – Транзакции. Временные таблицы, управляющие конструкции, циклы

1. Создайте функцию, которая принимает кол-во сек и форматирует их в кол-во дней, часов, минут и секунд.

    ```sql
    DELIMITER $$
    CREATE FUNCTION format_date(seconds INT)
    RETURNS TEXT
    DETERMINISTIC
    BEGIN
        DECLARE days INT;
        DECLARE hours INT;
        DECLARE minutes INT;
        DECLARE sec INT;

        SET days = FLOOR(seconds / (24 * 60 * 60));
        SET hours = FLOOR(seconds % (24 * 60 * 60) / (60 * 60));
        SET minutes = FLOOR(seconds % (60 * 60) / 60);
        SET sec = seconds % 60;
        
        IF days = 0 AND hours = 0 AND minutes = 0 THEN
            RETURN CONCAT(sec, ' seconds');
        ELSEIF days = 0 AND hours = 0 THEN
            RETURN CONCAT(minutes, ' minutes ', sec, ' seconds');
        ELSEIF days = 0 THEN
            RETURN CONCAT(hours, ' hours ', minutes, ' minutes ', sec, ' seconds');
        ELSE
            RETURN CONCAT(days, ' days ', hours, ' hours ', minutes, ' minutes ', sec, ' seconds');
        END IF;
    END $$
    DELIMITER ;
    ```

2. Выведите только четные числа от 1 до 10 включительно.

    ```sql
    DELIMITER $$

    CREATE FUNCTION show_even()
    RETURNS VARCHAR(30)
    DETERMINISTIC
    BEGIN
        DECLARE current INT DEFAULT 2;
        DECLARE stop INT DEFAULT 10;
        DECLARE result VARCHAR(30) DEFAULT '';

        WHILE current <= stop DO
            SET result = CONCAT(result, ' ', current);
            SET current =  current + 2;
        END WHILE;
        
        RETURN result;
    END $$
    DELIMITER ;
    ```
