**Hospital Patient Management System (MySQL)**

Project Creator: Anil Shingare
Contact: Alshingare22@gmail.com

📁 Project Description

Designed and implemented a Hospital Patient Management System using MySQL Workbench.
The project includes database schema design, creation of relational tables, sample data generation, advanced SQL queries, JOINS, stored procedures, views, and analytical reports for hospital operations.

🌟 🏗 Database Structure.

🌟 CREATE TABLE departments (
department_id INT PRIMARY KEY,
department_name VARCHAR(150) NOT NULL
) ENGINE=InnoDB;


🌟 CREATE TABLE doctors (
doctor_id INT PRIMARY KEY,
doctor_name VARCHAR(150) NOT NULL,
department_id INT,
phone VARCHAR(30),
CONSTRAINT fk_doctors_dept FOREIGN KEY (department_id) REFERENCES departments(department_id)
) ENGINE=InnoDB;


🌟 CREATE TABLE patients (
patient_id INT PRIMARY KEY,
first_name VARCHAR(100),
last_name VARCHAR(100),
gender VARCHAR(10),
date_of_birth DATE,
phone VARCHAR(30),
address TEXT
) ENGINE=InnoDB;


🌟CREATE TABLE rooms (
room_id INT PRIMARY KEY,
ward VARCHAR(50),
room_no VARCHAR(20),
bed_count INT
) ENGINE=InnoDB;


🌟 CREATE TABLE visits (
visit_id INT PRIMARY KEY,
patient_id INT,
doctor_id INT,
department_id INT,
admission_date DATE,
discharge_date DATE,
diagnosis VARCHAR(255),
severity VARCHAR(50),
referred VARCHAR(50),
billing_amount DECIMAL(12,2),
status VARCHAR(50),
CONSTRAINT fk_visits_patient FOREIGN KEY (patient_id) REFERENCES patients(patient_id),
CONSTRAINT fk_visits_doctor FOREIGN KEY (doctor_id) REFERENCES doctors(doctor_id),
CONSTRAINT fk_visits_dept FOREIGN KEY (department_id) REFERENCES departments(department_id)
) ENGINE=InnoDB;



⭐ Useful sample queries

🌟 Patient admitted history
SELECT p.first_name, p.last_name, v.admission_date, v.diagnosis
FROM patients p
JOIN visits v ON p.patient_id = v.patient_id
ORDER BY v.admission_date DESC
LIMIT 100;

🌟 Total revenue by department
SELECT d.department_name, SUM(v.billing_amount) AS total_revenue
FROM visits v
JOIN departments d ON v.department_id = d.department_id
GROUP BY d.department_name
ORDER BY total_revenue DESC;

🌟 Top 5 doctors by number of patients
SELECT doc.doctor_name, COUNT(*) AS total_cases
FROM visits v
JOIN doctors doc ON v.doctor_id = doc.doctor_id
GROUP BY doc.doctor_id, doc.doctor_name
ORDER BY total_cases DESC
LIMIT 5;

 🌟 Patients without any visits (LEFT JOIN)
SELECT p.*
FROM patients p
LEFT JOIN visits v ON p.patient_id = v.patient_id
WHERE v.visit_id IS NULL;

🌟 Simulate FULL OUTER JOIN (visits & patients)
SELECT v.*, p.*
FROM visits v
LEFT JOIN patients p ON v.patient_id = p.patient_id
UNION
SELECT v.*, p.*
FROM visits v
RIGHT JOIN patients p ON v.patient_id = p.patient_id;

🌟Stored procedure example

DELIMITER //
CREATE PROCEDURE GetDepartmentRevenue(IN dept INT)
BEGIN
SELECT d.department_name, SUM(v.billing_amount) AS total_revenue
FROM visits v
JOIN departments d ON v.department_id = d.department_id
WHERE d.department_id = dept
GROUP BY d.department_name;
END //
DELIMITER ;


🌟 I just completed a full SQL project using MySQL Workbench!

I built a Hospital Patient Management System with the following:

✔ Database schema (5 linked tables)
✔ Inserted 2000+ realistic records
✔ Performed advanced SQL queries (JOINs, AGGREGATION, SUBQUERIES)
✔ Created Views & Stored Procedures
✔ Built an ER Diagram
✔ Generated analytics reports: patient flow, doctor performance, revenue, severity levels, etc.

This project helped me improve:
🔹 SQL Joins (Left, Right, Inner, Full simulation)
🔹 Query optimization
🔹 Data modeling
🔹 MySQL Workbench skills






