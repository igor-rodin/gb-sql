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



2. Изменить в существующем представлении порог для стоимости: пусть цена будет до 30 000 долларов (используя оператор ALTER VIEW)

3. Создайте представление, в котором будут только автомобили марки “Шкода” и “Ауди”
