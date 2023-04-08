# Создание таблицы продуктов

CREATE TABLE `products` (  
   `id` int NOT NULL AUTO_INCREMENT,
   `name` varchar(45) NOT NULL,
   `price` decimal(5,2) NOT NULL,
   PRIMARY KEY (`id`)
 ) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
 
# Создание таблицы заказов
 
CREATE TABLE `orders` (
   `id` int NOT NULL AUTO_INCREMENT,
   `FIO` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `courier_id` int NOT NULL,
   PRIMARY KEY (`id`),
   KEY `orders_couriers_idx` (`courier_id`),
   CONSTRAINT `orders_couriers` FOREIGN KEY (`courier_id`) REFERENCES `couriers` (`id`)
 ) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
 
# Создание таблицы курьеров
 
 CREATE TABLE `couriers` (
   `id` int NOT NULL AUTO_INCREMENT,
   `name` varchar(45) NOT NULL,
   `phone_num` varchar(20) NOT NULL,
   `car_num` varchar(20) NOT NULL,
   PRIMARY KEY (`id`)
 ) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci

# Создание таблицы  order-item

CREATE TABLE `order_items` (
   `id` int NOT NULL AUTO_INCREMENT,
   `product_id` int NOT NULL,
   `order_id` int NOT NULL,
   `amount` int NOT NULL,
   PRIMARY KEY (`id`),
   KEY `products_order_items_idx` (`product_id`),
   KEY `orders_order_items_idx` (`order_id`),
   CONSTRAINT `orders_order_items` FOREIGN KEY (`order_id`) REFERENCES `orders` (`id`),
   CONSTRAINT `products_order_items` FOREIGN KEY (`product_id`) REFERENCES `products` (`id`)
 ) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
# 1. Получить всю информацию по ID заказа: продукты, количество, кто и куда доставляет, сумма заказа

SELECT o.FIO, o.address, p.name, oi.amount, p.price*oi.amount as Sum, c.name 
from shop.orders as o

join shop.couriers as c
on o.courier_id = c.id

join shop.order_items as oi
on o.id = oi.order_id

join shop.products as p
on p.id = oi.product_id

where o.id = 3


# 2. Создание заказа
INSERT INTO shop.orders (FIO, address, courier_id) VALUES ('Рита', 'Бутырина', '5');
INSERT INTO shop.order_items (product_id, order_id, amount) VALUES ('1', '3', '5');
INSERT INTO shop.order_items (product_id, order_id, amount) VALUES ('3', '4', '2');


# 3. Вывести все заказы для заданного ID курьера
SELECT x.FIO, x.address, p.name, oi.amount, p.priceoi.amount as Sum, c.name
FROM shop.orders as x

join shop.couriers as c
on x.courier_id = c.id

join shop.order_items as oi
on x.id = oi.order_id

join shop.products as p
on p.id = oi.product_id

where x.courier_id = 1


# 4. Увеличить количество продукта по имени продукта в конкретном заказе по ID
UPDATE shop.order_items
SET amount = '10'
WHERE (id = '3');
