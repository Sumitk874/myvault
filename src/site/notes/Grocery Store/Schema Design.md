---
{"dg-publish":true,"permalink":"/grocery-store/schema-design/"}
---

### Database creation
```SQL
CREATE DATABASE `grocery_store` /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci */ /*!80016 DEFAULT ENCRYPTION='N' */;
```
---
### Tables
#### Products
```sql
CREATE TABLE `products` (
  `product_id` int NOT NULL AUTO_INCREMENT,
  `product_name` varchar(45) NOT NULL,
  `unit_of_measure_id` int NOT NULL,
  `price_per_unit` double NOT NULL,
  PRIMARY KEY (`product_id`),
  KEY `fk_uom_id_idx` (`unit_of_measure_id`),
  CONSTRAINT `fk_uom_id` FOREIGN KEY (`unit_of_measure_id`) REFERENCES `unit_of_measure` (`unit_of_measure_id`) ON UPDATE RESTRICT
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

```

#### Orders
```sql
CREATE TABLE `orders` (
  `order_id` int NOT NULL AUTO_INCREMENT,
  `customer_name` varchar(60) NOT NULL,
  `total` double NOT NULL,
  `date` datetime NOT NULL,
  PRIMARY KEY (`order_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

#### Order_details
```sql
CREATE TABLE `order_details` (
  `order_id` int NOT NULL,
  `product_id` int NOT NULL,
  `quantity` double NOT NULL,
  `total_price` double NOT NULL,
  PRIMARY KEY (`order_id`),
  KEY `fk_product_id_idx` (`product_id`),
  CONSTRAINT `fk_order_id` FOREIGN KEY (`order_id`) REFERENCES `orders` (`order_id`) ON UPDATE RESTRICT,
  CONSTRAINT `fk_product_id` FOREIGN KEY (`product_id`) REFERENCES `products` (`product_id`) ON UPDATE RESTRICT
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```

#### Unit_of_measure
```sql
CREATE TABLE `unit_of_measure` (
  `unit_of_measure_id` int NOT NULL AUTO_INCREMENT,
  `unit_of_measure_name` varchar(45) NOT NULL,
  PRIMARY KEY (`unit_of_measure_id`)
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
```
---

