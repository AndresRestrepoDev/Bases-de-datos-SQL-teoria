# Bases-de-datos-SQL-teoria

Bases de datos SQL
=================

SQL
---

SQL (Structured Query Language) es el lenguaje estándar para gestionar bases de datos relacionales. Permite crear, consultar, actualizar y borrar datos, así como definir estructuras y permisos.

Motores ejemplos
----------------

- MySQL: Muy usado, open source, ideal para web.
- PostgreSQL: Robusto, estándar ANSI, soporte avanzado.
- SQLite: Ligero, embebido, ideal para apps pequeñas.
- MariaDB: Fork de MySQL con mejoras.

Gestores de base de datos
-------------------------

Herramientas para administrar bases de datos con interfaz gráfica o consola:

- DBeaver: Multiplataforma, soporta muchos motores.
- SQL Workbench/J: Ligero, en Java, ideal para scripting.

Categorías de comandos SQL
==========================

1. DDL (Data Definition Language): Definen estructuras.
   - CREATE, ALTER, DROP, TRUNCATE
2. DML (Data Manipulation Language): Manipulan datos.
   - SELECT, INSERT, UPDATE, DELETE
3. DCL (Data Control Language): Controlan permisos.
   - GRANT, REVOKE
4. TCL (Transaction Control Language): Control de transacciones.
   - COMMIT, ROLLBACK, SAVEPOINT
5. TCL (Task Control Language) o comandos adicionales
   - SHOW, DESCRIBE, USE

Restricciones o constraints
===========================

- PRIMARY KEY: Identificador único de filas.
- FOREIGN KEY: Referencia a otra tabla.
- UNIQUE: Valores únicos en columna.
- NOT NULL: No permite valores NULL.
- CHECK: Restricción condicional.
- DEFAULT: Valor por defecto.

Tipos de sentencias
===================

Cláusula de ordenamiento (ORDER BY)
-----------------------------------
Ordena resultados ascendente (ASC) o descendente (DESC).

Ejemplo:
SELECT * FROM clients ORDER BY name ASC;

Operadores condicionales
------------------------
=, <, >, <=, >=, <>, !=, BETWEEN, LIKE, IN, IS NULL

Cláusulas de agrupación y filtro (GROUP BY, HAVING)
---------------------------------------------------
Agrupa filas para funciones agregadas; HAVING filtra grupos.

Ejemplo:
SELECT genre, COUNT(*) FROM clients GROUP BY genre HAVING COUNT(*) > 1;

Cláusula de límite (LIMIT / OFFSET)
-----------------------------------
Limita la cantidad de resultados.

Ejemplo MySQL:
SELECT * FROM clients LIMIT 5 OFFSET 10;

Ejemplo PostgreSQL (igual sintaxis):

Cómo crear una base de datos
============================

MySQL y PostgreSQL:

CREATE DATABASE nombre_base;

Cómo usar una base de datos (USE)
=================================

MySQL:

USE nombre_base;

PostgreSQL:
No usa USE; se conecta directamente a la base deseada:

\c nombre_base

Cómo crear una tabla
====================

CREATE TABLE clients (
  id INT PRIMARY KEY AUTO_INCREMENT, -- SERIAL en PostgreSQL
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE,
  password VARCHAR(50),
  phone VARCHAR(50),
  address VARCHAR(100),
  genre VARCHAR(50)
);

En PostgreSQL se usa SERIAL para auto-incrementar:

id SERIAL PRIMARY KEY

Cómo crear claves foráneas y referenciarlas
===========================================

ALTER TABLE orders
ADD CONSTRAINT fk_client
FOREIGN KEY (client_id) REFERENCES clients(id);

Cómo insertar datos
===================

INSERT INTO clients (name, email, password, phone, address, genre)
VALUES ('Andres', 'andres@correo.com', '1234', '123456789', 'Calle 1', 'Masculino');

Consultas con SELECT
====================

SELECT * FROM clients;

Filtros y condiciones
=====================

SELECT * FROM clients WHERE genre = 'Masculino' AND phone IS NOT NULL;

JOINS
=====

INNER JOIN: Devuelve filas que coinciden en ambas tablas.

Ejemplo:
SELECT orders.id, clients.name
FROM orders
INNER JOIN clients ON orders.client_id = clients.id;

LEFT JOIN: Devuelve todas las filas de la izquierda y las coincidentes de la derecha.

Subconsultas
============

SELECT * FROM clients WHERE id IN (SELECT client_id FROM orders WHERE total > 100);

ALTER TABLE
===========

ALTER TABLE clients ADD COLUMN birthdate DATE;

Claves y restricciones
======================

CREATE TABLE example (
  id INT PRIMARY KEY,
  name VARCHAR(50) UNIQUE NOT NULL,
  age INT CHECK (age > 0)
);

Funciones agregadas
==================

COUNT(), SUM(), AVG(), MAX(), MIN()

Ejemplo:
SELECT genre, COUNT(*) FROM clients GROUP BY genre;

Triggers
========

Ejemplo básico MySQL:

CREATE TRIGGER before_insert_client
BEFORE INSERT ON clients
FOR EACH ROW
BEGIN
  SET NEW.name = UPPER(NEW.name);
END;

Control de acceso y transacciones
=================================

GRANT SELECT, INSERT ON lovelace.* TO 'user'@'localhost';

START TRANSACTION;
-- sentencias
COMMIT;
ROLLBACK;

Vistas
======

CREATE VIEW client_emails AS
SELECT name, email FROM clients;

Diferencias específicas MySQL y PostgreSQL
==========================================

- MySQL usa AUTO_INCREMENT, PostgreSQL SERIAL.
- PostgreSQL es más estricto con tipos y tiene más funciones avanzadas.
- PostgreSQL usa \c para conectar a bases, MySQL usa USE.
- PostgreSQL soporta JSONB, MySQL JSON.

Qué son las dependencias
========================

Son librerías o paquetes necesarios para conectar y manipular bases de datos desde lenguajes como Python o JavaScript.

Dependencias para usar bases de datos en Python y JS
====================================================

MySQL:
- Python: mysql-connector-python, pymysql, SQLAlchemy
- JS: mysql2, sequelize

PostgreSQL:
- Python: psycopg2, SQLAlchemy
- JS: pg, sequelize

Comandos útiles en consola
==========================

SHOW DATABASES;
SHOW TABLES;
DESCRIBE clients;
SELECT DATABASE();
SELECT VERSION();
