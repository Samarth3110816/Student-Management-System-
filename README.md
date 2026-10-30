# 🎓 Student Management System

![SQL Server](https://img.shields.io/badge/Database-SQL%20Server-red?style=for-the-badge&logo=microsoftsqlserver)
![SQL](https://img.shields.io/badge/Language-T--SQL-blue?style=for-the-badge)
![Project](https://img.shields.io/badge/Project-Database%20Management-green?style=for-the-badge)

## 📌 Project Overview

The **Student Management System** is a relational database project developed using Microsoft SQL Server. It manages student details, subject information, and academic marks.

The project demonstrates SQL development concepts such as database design, table relationships, constraints, joins, aggregate functions, views, and stored procedures.

## 🎯 Project Objectives

- Store and manage student information.
- Maintain subject details.
- Record student marks subject-wise.
- Retrieve student performance using SQL JOINs.
- Calculate average marks of students.
- Generate reusable database objects.

## 🛠️ Technologies Used

| Technology | Description |
|---|---|
| Microsoft SQL Server | Database management |
| T-SQL | Query language |
| SSMS | SQL development tool |

## 🗂️ Project Structure

```text
Student-Management-System/
│
├── README.md
│
└── project_students_management.sql
```

## 🏗️ Database Architecture

**Database Name:** `student_management`

The project contains three main tables:

### 1. Students Table

Stores student personal and academic information.

| Column | Description |
|---|---|
| student_id | Primary Key |
| student_name | Student Name |
| email | Student Email |
| course | Course Name |
| admission_date | Admission Date |

### 2. Subjects Table

Stores subject information.

| Column | Description |
|---|---|
| subject_id | Primary Key |
| subject_name | Subject Name |
| total_marks | Maximum Marks |

### 3. Marks Table

Stores student marks.

| Column | Description |
|---|---|
| mark_id | Primary Key |
| student_id | Foreign Key |
| subject_id | Foreign Key |
| marks_obtained | Marks Obtained |

## 🔗 Database Relationships

- One student can have multiple marks records.
- One subject can have multiple marks records.
- The Marks table connects Students and Subjects using foreign keys.

```text
Students (1) ───── (Many) Marks
Subjects (1) ───── (Many) Marks
```

## ⚙️ SQL Concepts Implemented

| SQL Concept | Implementation |
|---|---|
| DDL | CREATE DATABASE, CREATE TABLE |
| DML | INSERT |
| Constraints | PRIMARY KEY, FOREIGN KEY, UNIQUE, NOT NULL |
| Joins | INNER JOIN |
| Aggregate Functions | AVG(), ROUND() |
| Grouping | GROUP BY, ORDER BY |
| View | student_performance |
| Stored Procedure | GetStudentMarks |

## 📊 Key SQL Operations

### 1. Retrieve Student Details with Subject Marks

```sql
SELECT
    s.student_name,
    sub.subject_name,
    m.marks_obtained
FROM students s
INNER JOIN marks m
    ON s.student_id = m.student_id
INNER JOIN subjects sub
    ON m.subject_id = sub.subject_id;
```

### 2. Calculate Average Marks

```sql
SELECT
    s.student_name,
    ROUND(AVG(m.marks_obtained), 2) AS average_marks
FROM students s
INNER JOIN marks m
    ON s.student_id = m.student_id
GROUP BY s.student_id, s.student_name
ORDER BY average_marks DESC;
```

## 👁️ View – student_performance

Created a view to retrieve each student's average marks.

```sql
SELECT * FROM student_performance;
```

## ⚡ Stored Procedure – GetStudentMarks

Created a parameterized stored procedure to retrieve subject-wise marks for a particular student.

**Execution:**

```sql
EXEC GetStudentMarks @studentId = 1;
```

## 🚀 How to Execute the Project

1. Install Microsoft SQL Server.
2. Open SQL Server Management Studio (SSMS).
3. Connect to your SQL Server instance.
4. Open the project SQL script.
5. Execute the complete SQL script.
6. Verify the database and tables.
7. Execute the SELECT queries, view, and stored procedure.

## 📈 Sample Project Data

- Students: 3
- Subjects: 3
- Marks Records: 9

## 🔮 Future Enhancements

- Implement database triggers.
- Create indexes for query optimization.
- Add UPDATE and DELETE operations.
- Add validation for marks and duplicate entries.
- Develop student performance reports.
- Integrate with a front-end application.

## 🎓 Learning Outcomes

- Relational database design.
- SQL query writing and optimization fundamentals.
- Table relationships and constraints.
- Data retrieval using JOINs.
- Aggregate functions and grouping.
- Creating views and stored procedures.

---

## 👨‍💻 Author

**Samarth Bhosale**

SQL Developer | SQL Server | T-SQL

⭐ If you find this project useful, feel free to explore the repository!

