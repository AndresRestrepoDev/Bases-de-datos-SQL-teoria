# Bases-de-datos-SQL-teoria

📚 Guía de Referencia Rápida: Bases de Datos SQL¡Bienvenido a esta guía completa sobre Bases de Datos Relacionales y SQL! Este documento te servirá como una referencia rápida para entender los conceptos clave y los comandos más importantes.💻 SQL (Structured Query Language)SQL es el lenguaje estándar para gestionar bases de datos relacionales. Te permite manipular, consultar y definir la estructura de los datos, así como gestionar permisos de acceso.⚙️ Ejemplos de Motores de Bases de DatosMotorCaracterísticasUso IdealMySQLOpen source, muy popular y de alto rendimiento.Aplicaciones web, CMS.PostgreSQLMuy robusto, compatible con estándares ANSI, con soporte avanzado.Sistemas de misión crítica, análisis de datos complejos.SQLiteLigero, sin servidor, embebido en la aplicación.Aplicaciones móviles, archivos de configuración.MariaDBFork de MySQL con mejoras de rendimiento.Reemplazo directo para MySQL.🛠️ Gestores de Bases de DatosHerramientas para administrar bases de datos con una interfaz gráfica:DBeaver: Multiplataforma y soporta una amplia variedad de motores.SQL Workbench/J: Ligero, basado en Java, excelente para scripting.📖 Categorías de Comandos SQLLos comandos se dividen en categorías según su función:DDL (Data Definition Language): Para definir la estructura de la base de datos.CREATE, ALTER, DROP, TRUNCATE
DML (Data Manipulation Language): Para manipular los datos.SELECT, INSERT, UPDATE, DELETE
DCL (Data Control Language): Para controlar permisos.GRANT, REVOKE
TCL (Transaction Control Language): Para controlar transacciones.COMMIT, ROLLBACK, SAVEPOINT
Comandos adicionales:SHOW, DESCRIBE, USE
🔒 Restricciones (Constraints)Las restricciones garantizan la integridad de los datos en las tablas:PRIMARY KEY: Identificador único de filas.FOREIGN KEY: Referencia a otra tabla.UNIQUE: Los valores en la columna deben ser únicos.NOT NULL: La columna no puede tener valores nulos.CHECK: Restricción condicional que debe cumplirse.DEFAULT: Valor por defecto para la columna.📋 Ejemplos de Sentencias SQL📊 Cláusula de ordenamiento (ORDER BY)Ordena los resultados en forma ascendente (ASC) o descendente (DESC).SELECT * FROM clients ORDER BY name ASC;
🧩 Operadores condicionales=, <, >, <=, >=, <>, !=, BETWEEN, LIKE, IN, IS NULL
📈 Cláusulas de agrupación y filtro (GROUP BY, HAVING)GROUP BY agrupa filas para funciones agregadas; HAVING filtra los grupos.SELECT genre, COUNT(*) FROM clients GROUP BY genre HAVING COUNT(*) > 1;
➡️ Cláusula de límite (LIMIT / OFFSET)Limita la cantidad de resultados devueltos.-- Ejemplo MySQL
SELECT * FROM clients LIMIT 5 OFFSET 10;
🏗️ Creación y ManipulaciónCrear una base de datos-- MySQL y PostgreSQL
CREATE DATABASE nombre_base;
Usar una base de datos-- MySQL
USE nombre_base;

-- PostgreSQL (se usa un comando de la consola)
\c nombre_base
Crear una tablaCREATE TABLE clients (
  id INT PRIMARY KEY AUTO_INCREMENT, -- SERIAL en PostgreSQL
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE,
  password VARCHAR(50),
  phone VARCHAR(50),
  address VARCHAR(100),
  genre VARCHAR(50)
);

-- Sintaxis para PostgreSQL
id SERIAL PRIMARY KEY
Crear claves foráneas y referenciarlasALTER TABLE orders
ADD CONSTRAINT fk_client
FOREIGN KEY (client_id) REFERENCES clients(id);
Insertar datosINSERT INTO clients (name, email, password, phone, address, genre)
VALUES ('Andres', 'andres@correo.com', '1234', '123456789', 'Calle 1', 'Masculino');
🔎 Consultas y RelacionesConsultas con SELECTSELECT * FROM clients;
Filtros y condicionesSELECT * FROM clients WHERE genre = 'Masculino' AND phone IS NOT NULL;
JOINSCombina filas de dos o más tablas en una sola consulta.INNER JOIN: Devuelve filas que coinciden en ambas tablas.SELECT orders.id, clients.name
FROM orders
INNER JOIN clients ON orders.client_id = clients.id;
LEFT JOIN: Devuelve todas las filas de la tabla de la izquierda y las coincidentes de la derecha.SubconsultasSELECT * FROM clients WHERE id IN (SELECT client_id FROM orders WHERE total > 100);
ALTER TABLEPara modificar la estructura de una tabla existente.ALTER TABLE clients ADD COLUMN birthdate DATE;
Funciones agregadasFunciones que operan sobre un conjunto de filas (COUNT(), SUM(), AVG(), MAX(), MIN()).SELECT genre, COUNT(*) FROM clients GROUP BY genre;
🧩 Herramientas y DiferenciasTriggersEjecutan un procedimiento almacenado en respuesta a un evento (INSERT, UPDATE, DELETE).-- Ejemplo básico en MySQL
CREATE TRIGGER before_insert_client
BEFORE INSERT ON clients
FOR EACH ROW
BEGIN
    SET NEW.name = UPPER(NEW.name);
END;
Control de acceso y transaccionesGRANT SELECT, INSERT ON lovelace.* TO 'user'@'localhost';

START TRANSACTION;
-- sentencias
COMMIT;
ROLLBACK;
VistasUna vista es una tabla virtual basada en el resultado de una consulta.CREATE VIEW client_emails AS
SELECT name, email FROM clients;
Diferencias específicas entre MySQL y PostgreSQLAuto-incremento: MySQL usa AUTO_INCREMENT, mientras que PostgreSQL usa SERIAL.Sintaxis: PostgreSQL usa \c para conectar a bases de datos, mientras que MySQL usa USE.Tipos de datos: PostgreSQL es más estricto con los tipos y tiene más funciones avanzadas.DependenciasLibrerías o paquetes necesarios para conectar a bases de datos desde un lenguaje de programación.MotorPythonJavaScript (Node.js)MySQLmysql-connector-python, pymysqlmysql2, sequelizePostgreSQLpsycopg2, SQLAlchemypg, sequelizeComandos útiles en consolaSHOW DATABASES;
SHOW TABLES;
DESCRIBE clients;
SELECT DATABASE();
SELECT VERSION();
