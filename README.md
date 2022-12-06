# Базы данных и SQL (семинары)

## Урок 5. SQL – оконные функции

Импорт в таблицу cars из csv файла

```sql
    USE lesson_5;

    CREATE TABLE cars
    (
        id INT UNSIGNED NOT NULL PRIMARY KEY,
        name VARCHAR(20),
        cost INT UNSIGNED
    );

    SET GLOBAL local_infile = 1;

    LOAD DATA LOCAL INFILE '/Users/igor-rodin/work/test_db.csv'
    INTO TABLE cars
    FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    IGNORE 1 ROWS;
```

1. Создайте представление, в которое попадут автомобили стоимостью  до 25 000 долларов

    ```sql
    use lesson_5;

    CREATE VIEW cheap_cars AS 
    SELECT id, `name`, cost
    FROM cars
    WHERE cost < 25000;
    ```

2. Изменить в существующем представлении порог для стоимости: пусть цена будет до 30 000 долларов (используя оператор ALTER VIEW)

    ```sql
    use lesson_5;

    ALTER VIEW cheap_cars AS
    SELECT id, `name`, cost
    FROM cars
    WHERE cost < 30000;
 
    ```

3. Создайте представление, в котором будут только автомобили марки “Шкода” и “Ауди”

    ```sql
    use lesson_5;

    CREATE VIEW skoda_audi_cars AS
    SELECT id, `name`, cost
    FROM cars
    WHERE `name` IN ("Skoda", "Audi");
    ```

4. Добавьте новый столбец под названием «время до следующей станции». Чтобы получить это значение, мы вычитаем время станций для пар смежных станций. Мы можем вычислить это значение без использования оконной функции SQL, но это может быть очень сложно. Проще это сделать с помощью оконной функции LEAD . Эта функция сравнивает значения из одной строки со следующей строкой, чтобы получить результат. В этом случае функция сравнивает значения в столбце «время» для станции со станцией сразу после нее.

    ```sql
    use lesson_5;
    -- Создание таблицы
    CREATE TABLE stations
    (
    train_id INT NOT NULL,
        station varchar(20) NOT NULL,
        station_time TIME NOT NULL
    );

    INSERT stations(train_id, station, station_time)
    VALUES (110, "SanFrancisco", "10:00:00"),
            (110, "Redwood Sity", "10:54:00"),
            (110, "Palo Alto", "11:02:00"),
            (110, "San Jose", "12:35:00"),
            (120, "SanFrancisco", "11:00:00"),
            (120, "Palo Alto", "12:49:00"),
            (120, "San Jose", "13:30:00");

    -- Время до следующей станции
    SELECT train_id, station, station_time,
    TIMEDIFF(LEAD(station_time) OVER(PARTITION BY train_id), station_time) AS time_to_next_station
    FROM stations;
    ```
