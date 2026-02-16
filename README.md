# goit-rdb-hw-02
Database design using semantic models - SQL
This is a professional **README.md** tailored to your project. It explains the normalization process, the transition to 3NF, and the technical implementation in MySQL Workbench.

---

# Relational Database Normalization Project

## Project Overview

This project demonstrates the process of transforming a "flat" unnormalized database table into a structured, relational database following the **Third Normal Form (3NF)**. The primary goal was to eliminate data redundancy and ensure data integrity within an Order Management System.

## Database Evolution

### 1. Initial State (1NF)

The original table contained all data in a single sheet, leading to significant redundancy (e.g., client names and addresses were repeated for every item in an order).

### 2. Normalization to 2NF & 3NF

To achieve a professional schema, the data was decomposed into three logical entities:

* **`clients`**: Stores unique customer information.
* **`orders_info`**: Stores general order data (dates, order numbers) and links to a client.
* **`order_details`**: Stores specific items within an order, preventing the duplication of order headers for every product.

## Entity Relationship (ER) Diagram

The database structure was visualized using a **Model-First** approach in MySQL Workbench.

### Key Relationships:

* **Clients to Orders (`1:N`)**: One client can place multiple orders. Linked via `client_id`.
* **Orders to Order Details (`1:N`)**: One order can contain multiple line items. Linked via `number_order`.

---

## Technical Implementation

### Technologies Used

* **Database Engine**: MySQL 8.0
* **Modeling Tool**: MySQL Workbench (EER Diagrammer)
* **Language**: SQL

### Schema Structure

The final schema consists of the following tables:

1. **`clients`**: `id` (PK), `client_name`, `client_adress`.
2. **`orders_info`**: `id` (PK), `number_oder`, `date_order`, `client_id` (FK).
3. **`order_details`**: `id_order` (PK), `number_order` (FK), `name_goods`, `quantity_goods`.

### SQL Generation

The physical database was generated using the **Forward Engineering** tool, which automatically translated the ER Diagram into a high-performance SQL script.

```sql
-- Example of the generated structure
CREATE TABLE IF NOT EXISTS `orders_info` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `number_oder` INT NULL,
  `date_order` DATE NULL,
  `client_id` INT NULL,
  PRIMARY KEY (`id`),
  CONSTRAINT `fk_order_client`
    FOREIGN KEY (`client_id`)
    REFERENCES `clients` (`id`)
);

```

## How to Run

1. Open **MySQL Workbench**.
2. Run the provided `Forward Engineer` script to recreate the schema.
3. The database is ready for data entry with full referential integrity.

---

