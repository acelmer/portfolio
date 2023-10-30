#  Car Dealership
### Create an ERD for a car dealership. The dealership sells both new and used cars, and it operates a service facility. Base your design on the following business rules:
- A salesperson may sell many cars, but each car is sold by only one salesperson.
- A customer may buy many cars, but each car is bought by only one customer.
- A salesperson writes a single invoice for each car he or she sells.
- A customer gets an invoice for each car he or she buys.
- A customer may come in just to have his or her car serviced; that is, a customer need not buy a car to be classified as a customer.
- When a customer takes one or more cars in for repair or service, one service ticket is written for each car.
- The car dealership maintains a service history for each of the cars serviced. The service  records are referenced by the car’s serial number.
- A car brought in for service can be worked on by many mechanics, and each mechanic may work on many cars.
- A car that is serviced may or may not need parts (e.g., adjusting a carburetor or cleaning a fuel injector nozzle does not require providing new parts).

```sql
CREATE TABLE "Salesperson"(
	salesperson_id INT PRIMARY KEY,
	last_name VARCHAR(30) NOT NULL,
	first_name VARCHAR(20) NOT NULL
);
```
```sql
CREATE TABLE "Car"(
	car_id INT PRIMARY KEY,
	serial_number VARCHAR(30) NOT NULL,
	make VARCHAR(20) NOT NULL,
	model VARCHAR(20) NOT NULL,
	colour VARCHAR(10) NOT NULL,
	YEAR INT NOT NULL,
    for_sale BOOLEAN NOT NULL
);
```
```sql
CREATE TABLE "Customer"(
	customer_id INT PRIMARY KEY,
	last_name VARCHAR(30) NOT NULL,
	first_name VARCHAR(20) NOT NULL,
	phone_number INT NOT NULL,
	address VARCHAR(30)NOT NULL,
	city INT NOT NULL,
	state VARCHAR(20)NOT NULL,
	country VARCHAR(20) NOT NULL,
	postal_code INT
);
```
```sql
CREATE TABLE "Sales_Invoice"(
	invoice_id INT PRIMARY KEY,
	invoice_number VARCHAR(60) NOT NULL,
	date DATE NOT NULL,
	car_id INT REFERENCES "Car"(car_id)NOT NULL,
	customer_id INT REFERENCES "Customer"(customer_id) NOT NULL,
	salesperson_id INT REFERENCES "Salesperson"(salesperson_id) NOT NULL
);
```
```sql
CREATE TABLE "Mechanic"(
	mechanic_id INT PRIMARY KEY,
	last_name VARCHAR(30) NOT NULL,
	first_name VARCHAR(20) NOT NULL
);
```
```sql
CREATE TABLE "Service_Ticket"(
	service_ticket_id INT PRIMARY KEY,
	service_ticket_number INT NOT NULL,
	car_id INT REFERENCES "Car"(car_id)NOT NULL,
	customer_id INT REFERENCES "Customer"(customer_id) NOT NULL,
	date_received DATE NOT NULL	
);
```
```sql
CREATE TABLE "Service"(
	service_id INT PRIMARY KEY,
	service_name VARCHAR(30) NOT NULL,
	hourly_rate INT NOT NULL
);
```
```sql
CREATE TABLE "Parts"(
	part_id INT PRIMARY KEY,
	part_number INT NOT NULL,
	description VARCHAR(30) NOT NULL,
	purchase_price INT NOT NULL,
	retail_price INT NOT NULL
);
```
```sql
CREATE TABLE "Used_Parts"(
	used_part_id INT PRIMARY KEY,
	part_id INT REFERENCES "Parts"(part_id) NOT NULL,
	service_ticket_id INT REFERENCES "Service_Ticket"(service_ticket_id) NOT NULL,
	price INT NOT NULL
);
```
```sql
CREATE TABLE "Service_Mechanic"(
	service_mechanic_id INT PRIMARY KEY,
	service_ticket_id INT REFERENCES "Service_Ticket"(service_ticket_id) NOT NULL,
	service_id INT REFERENCES "Service"(service_id) NOT NULL,
	mechanic_id INT REFERENCES "Mechanic"(mechanic_id) NOT NULL,
	hours INT NOT NULL
);
```


<p align="center">
<img src="https://github.com/acelmer/portfolio/assets/145276189/5e7cac9d-95b4-4a3f-b55e-4455b7d4ca72" width=100% height=100%>
</p>
