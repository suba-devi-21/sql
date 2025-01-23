Create a database named ecommerce.
create database ecommerce;
use ecommerce;
Customers table.
create table customers(id int primary key auto_increment,name varchar(20),email varchar(20),address varchar(50));

desc customers;
Customers table Data.
insert into customers values
 (1,"suba","suba@gmail.com","namakkal"),
 (2,"ricky","ricky@gmail.com","salem"),
 (3,"gokul","gokul@gmail.com","erode"),
 (4,"hari","hari@gmail.com","namakkal"),
 (5,"kayal","kayal@gmail.com","chennai"),
 (6,"raj","raj@gmail.com","chennai"),
 (7,"sowndharya","sowndharya@gmail.com","namakkal"),
 (8,"vel","vel@gmail.com","karraikudi"),
 (9,"vijay","vijay@gmail.com","karraikudi"),
 (10,"sakthi","sakthi@gmail.com","salem");
select * from customers;
orders Table
create table  orders(id int primary key auto_increment,customer_id int references customers(id),order_date date ,total_amount int)	;

desc orders;
orders table Data.
insert into orders values
 (1,1,"2024-10-2",50),
 (2,2,"2024-10-12",150),
 (3,1,"2024-11-6",200),
 (4,5,"2024-11-28",350),
 (5,5,"2024-10-25",333),
 (6,8,"2024-12-5",99),
 (7,4,"2024-12-11",66),
 (8,3,"2024-11-28",73),
 (9,6,"2024-12-21",64),
 (10,6,"2024-12-9",82),
 (11,7,"2024-11-30",100),
 (12,10,"2024-11-10",173);
select * from orders;
products Table
create table products(id int primary key auto_increment,name varchar(20),price int,description varchar(50));

desc products;
Products table Data.
insert into products values
(1,"product A",111,"vegicles"),
(2,"product B",222,"groceries"),
(3,"product c",100,"vegetables"),
(4,"product d",555,"cloths"),
(5,"product e",666,"furnuiture"),
(6,"product c",444,"electronics");
select * from products;
view table with data.
select * from products;
select * from orders;
select * from customers;


                          **Queries **


1) Retrieve all customers who have placed an order in the last 30 days.
select distinct customers.id, customers.name,customers.email,customers.address
from customers
join orders
on customers.id = orders.customer_id
where order_date >=curdate()- interval 30 day;

2) Get the total amount of all orders placed by each customer.
SELECT customers.id, customers.name, customers.email, customers.address, SUM(orders.total_amount) AS Total_amount
FROM customers
JOIN orders ON customers.id = orders.customer_id
GROUP BY customers.id;

3) Update the price of Product C to 45.00.
select * from products;
update products set price=45 where id=3;
select * from products;

4) Add a new column discount to the products table.
alter table products add column discount int;
select * from products;

5) Retrieve the top 3 products with the highest price.
select * from products;
select * from products order by price desc limit 3;

6) Get the names of customers who have ordered Product A.
-- table list
select * from customers;
select * from products;
select * from orders;
select * from order_items;

SELECT DISTINCT customers.name
FROM customers
JOIN orders ON customers.id = orders.customer_id
JOIN order_items ON orders.id = order_items.order_id
JOIN products ON products.id = order_items.product_id
WHERE products.name = 'Product a';

7) Join the orders and customers tables to retrieve the customer's name and order date for each order.
 select orders.id as order_id ,customers.name as customer_Name,orders.order_date
   from orders
   join customers
   ON
   customers.id = orders.customer_id;

8) Retrieve the orders with a total amount greater than 150.00.
select * from orders
where total_amount >150;

9) Normalize the database by creating a separate table for order items and updating the orders table to reference the order_items table.
CREATE TABLE order_items (
 id INT AUTO_INCREMENT PRIMARY KEY,
 order_id INT,
 product_id INT,
 foreign key (order_id) references orders(id),
 foreign key (product_id) references products(id)
);
desc order_items;
select * from order_items;

10) Retrieve the average total of all orders.
SELECT AVG(total_amount) as average_total
FROM orders;