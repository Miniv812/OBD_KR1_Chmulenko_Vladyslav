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

```
