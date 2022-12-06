# Базы данных и SQL (семинары). Дополнительные задачи

1. Вывести марку и цвет автомобиля - имя и фамилию покупателя, для всех покупателей, которые живут в городе с населением больше  1 млн человек.

    ```sql
        select a.mark, a.color, m.firstname, m.lastname 
        from auto a inner join 
            (select m.firstname, m.lastname, m.phonenum from man m
            inner join city c
            on m.citycode = c.citycode
            where c.peoples > 1000000) m
        on a.phonenum = m.phonenum;


        -- второй способ
        select a.mark, a.color, m.firstname, m.lastname
        from auto a inner join man m
        on a.phonenum = m.phonenum
        inner join city c
        on m.citycode = c.citycode
        where c.peoples > 1000000;
    ```

2. Вывести на экран людей которые живут в городах с населением больше 1_000_000, если людей с таким же именем нет в таблице MAN.

    ```sql
        select m.firstname, m.lastname
        from man m inner join
        (
            select citycode from city
            where peoples > 1000000
        ) c
        on m.citycode = c.citycode
        where m.firstname not in
        (select firstname from man
        where m.phonenum <> phonenum);
    ```

3. Вывести на экран города если в таблице нет города который начинается на такую же букву.

    ```sql
        select c.cityname
        from city c
        where left(c.cityname, 1) not in
        (
            select left(cityname, 1) from city
            where citycode <> c.citycode
        );
    ```

4. Вывести на экран сколько машин каждого цвета  для машин марок BMW и LADA.

    ```sql
        select mark, color, count(color) as count_color from auto
        where mark in ('BMW', 'LADA')
        group by color, mark
        order by mark;
    ```

5. Подсчитать количество BMW в AUTO.

    ```sql
        select mark, count(mark) as count_mark from auto
        where mark = 'BMW';
    ```

6. Вывести на экран марку авто и количество AUTO не этой марки.

    ```sql
        select distinct(mark), 
        (count(mark) over() - 
            count(mark) over(partition by mark)) as count_other_mark from auto
        order by mark;
    ```
