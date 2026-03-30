```sql
create type hotel_stars as enum('1 Зірка','2 Зірки','3 Зірки','4 Зірки','5 Зірок <3');

CREATE TABLE if not exists hotel(
	hotel_id SERIAL PRIMARY KEY,
	hotel_name varchar(100) NOT NULL,
	hotel_star hotel_stars NOT NULL,
	hotel_city varchar(100) NOT NULL,
	hotel_adress varchar(120) NOT NULL
);

CREATE TABLE if not exists room_type(
	type_id SERIAL PRIMARY KEY,
	type_name varchar(50) NOT NULL UNIQUE,
	capacity int NOT NULL CHECK (capacity > 0),
	price numeric(10,2) NOT NULL CHECK (price >= 0),
	description text
);

CREATE TABLE if not exists room(
	room_id SERIAL PRIMARY KEY,
	room_number int NOT NULL check (room_number > 0),
	hotel_id int NOT NULL references hotel(hotel_id),
	room_type int NOT NULL references room_type(type_id),
	UNIQUE (hotel_id, room_number)
);

CREATE TABLE if not exists customers(
	customer_id SERIAL PRIMARY KEY,
	customer_name varchar(50) NOT NULL,
	customer_surname varchar(80),
	customer_phone varchar(20) NOT NULL UNIQUE,
	customer_email varchar(100) NOT NULL UNIQUE,
	customer_password varchar(100) NOT NULL
);

create type reservations_status as enum ('Заброньовано','Скасовано','Завершено');

CREATE TABLE if not exists reservation(
	reservation_id SERIAL PRIMARY KEY,
	check_in_date DATE NOT NULL,
	check_out_date DATE NOT NULL,
	number_of_customers int NOT NULL CHECK (number_of_customers > 0),
	reservation_status reservations_status NOT NULL,
	customer_id int references customers(customer_id),
	room_id int references room(room_id),
	CHECK (check_out_date > check_in_date)
);
```
