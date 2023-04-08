#Создание таблицы продуктов

CREATE TABLE `products` (
   `id` int NOT NULL AUTO_INCREMENT,
   `name` varchar(45) NOT NULL,
   `price` decimal(5,2) NOT NULL,
   PRIMARY KEY (`id`)
 ) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
 
#Создание таблицы заказов
 
CREATE TABLE `orders` (
   `id` int NOT NULL AUTO_INCREMENT,
   `FIO` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `courier_id` int NOT NULL,
   PRIMARY KEY (`id`),
   KEY `orders_couriers_idx` (`courier_id`),
   CONSTRAINT `orders_couriers` FOREIGN KEY (`courier_id`) REFERENCES `couriers` (`id`)
 ) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
 
#Создание таблицы курьеров
 
 CREATE TABLE `couriers` (
   `id` int NOT NULL AUTO_INCREMENT,
   `name` varchar(45) NOT NULL,
   `phone_num` varchar(20) NOT NULL,
   `car_num` varchar(20) NOT NULL,
   PRIMARY KEY (`id`)
 ) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci
