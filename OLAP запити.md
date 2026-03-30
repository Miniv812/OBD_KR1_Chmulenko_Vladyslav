Знайти середню тривалість бронювання за типом номера:

```sql
SELECT 
    rt.type_name,
    AVG(res.check_out_date - res.check_in_date) AS avg_nights
FROM reservation res
JOIN room r ON res.room_id = r.room_id
JOIN room_type rt ON r.room_type = rt.type_id
GROUP BY rt.type_name;
```

<img width="454" height="153" alt="{3A05E9E3-A7B8-4DDA-8509-166DEE17F24C}" src="https://github.com/user-attachments/assets/b628ed85-1e08-4def-92cc-49b8d8452a5e" />


Показати помісячний дохід за готелем за минулий рік:

```sql
SELECT 
    h.hotel_name,
    DATE_TRUNC('month', res.check_in_date) AS month,
    SUM(rt.price * (res.check_out_date - res.check_in_date)) AS total_income
FROM reservation res
JOIN room r ON res.room_id = r.room_id
JOIN hotel h ON r.hotel_id = h.hotel_id
JOIN room_type rt ON r.room_type = rt.type_id
WHERE EXTRACT(YEAR FROM res.check_in_date) = EXTRACT(YEAR FROM CURRENT_DATE) - 1
GROUP BY h.hotel_name, DATE_TRUNC('month', res.check_in_date)
ORDER BY h.hotel_name, month;
```

<img width="621" height="156" alt="{F3FEF122-06F5-4D45-8739-546A8BC2C845}" src="https://github.com/user-attachments/assets/7d813821-036d-4bfe-af2e-9ff32329628c" />

Ранжувати готелі за загальною кількістю бронювань (віконні функції):

```sql
SELECT 
    h.hotel_name,
    COUNT(res.reservation_id) AS total_reservations,
    RANK() OVER (ORDER BY COUNT(res.reservation_id) DESC) AS hotel_rank
FROM hotel h
JOIN room r ON h.hotel_id = r.hotel_id
JOIN reservation res ON r.room_id = res.room_id
GROUP BY h.hotel_id, h.hotel_name
ORDER BY hotel_rank;
```

<img width="552" height="141" alt="{B2FD5ED3-3228-411F-86CE-1BA68781DD49}" src="https://github.com/user-attachments/assets/3f22bb7c-12aa-4695-941b-1bd6fc8d06a1" />


Визначити гостей, які зробили декілька бронювань, але скасували всі (CTE):

```sql
WITH customer_stats AS (
    SELECT 
        c.customer_id,
        c.customer_name,
        c.customer_surname,
        COUNT(res.reservation_id) AS total_reservations,
        SUM(CASE WHEN res.reservation_status = 'Скасовано' THEN 1 ELSE 0 END) AS cancelled_reservations
    FROM customers c
    JOIN reservation res ON c.customer_id = res.customer_id
    GROUP BY c.customer_id, c.customer_name, c.customer_surname
)

SELECT 
    customer_id,
    customer_name,
    customer_surname,
    total_reservations
FROM customer_stats
WHERE total_reservations > 1
  AND total_reservations = cancelled_reservations;
```

<img width="724" height="139" alt="{59CF8C7A-7C3D-4E5A-8CD7-E3D4335FB620}" src="https://github.com/user-attachments/assets/89401c84-73fa-449d-bbef-08d4fdc1fb53" />


