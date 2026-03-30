INSERT:

```sql
INSERT INTO hotel(hotel_name, hotel_star, hotel_city, hotel_adress)
VALUES ('Anna de Mari', '5 Зірок <3', 'Київ', 'бульвар Тараса Шевченка 13'),
('Bugget Ink', '4 Зірки', 'Харків', 'вул. Дрогобичі 21');

INSERT INTO room_type(type_name, capacity, price, description)
VALUES ('Одномісний', 1, 800, 'Для однієї людини'),
('Двомісний', 2, 1200, 'Для двох людей'),
('Люкс', 3, 2500, 'Покращений номер'),
('Пентхаус', 5, 5000, 'Найкращий номер');

INSERT INTO room(room_number, hotel_id, room_type)
VALUES (101, 9, 17),
(102, 9, 18),
(101, 10, 19),
(201, 10, 19),
(202, 10, 20)

INSERT INTO customers(customer_name, customer_surname, customer_phone, customer_email, customer_password)
VALUES ('Іван', 'Іваненко', '+380 50 777 77 77', 'ivan@gmail.com', '123123'),
('Тарасік', 'Дутов', '+380 50 222 52 52', 'abugren@gmail.com', 'slowpet123'),
('Владислав', 'Чмуленко', '+380 66 951 33 48', 'vladchmulenko@gmail.com', '************');

INSERT INTO reservation(check_in_date, check_out_date, number_of_customers, reservation_status, customer_id, room_id)
VALUES ('2026-04-01', '2026-04-05', 1, 'Заброньовано', 2, 21),
('2026-04-10', '2026-04-15', 2, 'Завершено', 3, 25)
```


UPDATE:

```sql
UPDATE room 
SET room_number = 105 
WHERE room_number = 101;
SELECT * FROM room

UPDATE customers
SET customer_phone = '+380 50 777 52 42'
WHERE customer_phone = '+380 50 777 77 77';
SELECT (customer_phone) FROM customers
```

DELETE: 

```sql
DELETE FROM room
WHERE room_number >= 500;
SELECT * FROM room

DELETE FROM customers
WHERE customer_id = 1;
SELECT * FROM customers
```

SELECT:

знайти всі доступні номери в готелі на конкретні дати:

```sql
SELECT * FROM room r
WHERE r.room_id NOT IN (
    SELECT res.room_id
    FROM reservation res
    WHERE 
        res.check_in_date < '2026-04-06'
        AND res.check_out_date > '2026-04-02'
);
```

<img width="539" height="235" alt="{53D5BE1E-F17D-49D3-AFA0-AED5B0E26086}" src="https://github.com/user-attachments/assets/0a995498-5960-4ed3-b7b3-a57d0273dc2a" />


обчислити загальну вартість для бронювання:

```sql
SELECT 
    res.reservation_id,
    r.room_number,
    rt.type_name,
    rt.price,
    (res.check_out_date - res.check_in_date) AS nights,
    rt.price * (res.check_out_date - res.check_in_date) AS total_price
FROM reservation res
JOIN room r ON res.room_id = r.room_id
JOIN room_type rt ON r.room_type = rt.type_id;
```

<img width="858" height="144" alt="{1D4027A1-974F-4D18-9B1B-F82C4A3B2908}" src="https://github.com/user-attachments/assets/ef57dcfd-87a0-4cad-88dd-a41a3fc084ca" />

