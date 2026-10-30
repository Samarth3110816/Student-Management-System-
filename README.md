Student Management System
A relational database project developed using Microsoft SQL Server (T-SQL) to manage student information, subjects, and academic marks. The project demonstrates database creation, table relationships, data insertion, joins, aggregate queries, a view, and a stored procedure.
1. Project Overview
The Student Management System stores student details, subject details, and marks obtained by students. It allows users to retrieve marks subject-wise and calculate each student's average marks.
Objectives
- Store and organize student information.
- Maintain a list of subjects.
- Record marks obtained by each student in each subject.
- Retrieve student marks along with subject names.
- Calculate average marks and compare student performance.
- Demonstrate the use of SQL Server database objects.
2. Technologies Used
- Database: Microsoft SQL Server
- Query Language: T-SQL
- Database Tool: SQL Server Management Studio (SSMS)
3. Repository Structure
Student-Management-System/
│
├── README.md
│   └── Project documentation and setup instructions
│
└── project_students_management.sql
    └── Database creation, table definitions, sample data,
        queries, view, and stored procedure
Keep the SQL script in the repository root and use the filename shown above, or update the filename in this documentation to match the name you actually upload.

4. Database Structure
Database name: student_management

The database contains three tables:
4.1 students
Stores basic student information.
Column	Data type	Constraint	Description
student_id	INT	Primary Key, IDENTITY(1,1)	Unique student ID
student_name	VARCHAR(100)	NOT NULL	Student name
email	VARCHAR(100)	UNIQUE	Student email
course	VARCHAR(50)	—	Course name
admission_date	DATE	—	Admission date


4.2 subjects
Stores subject information and maximum marks.
Column	Data type	Constraint	Description
subject_id	INT	Primary Key, IDENTITY(1,1)	Unique subject ID
subject_name	VARCHAR(100)	NOT NULL	Subject name
total_marks	INT	—	Maximum marks for the subject


4.3 marks
Stores marks obtained by students in individual subjects.
Column	Data type	Constraint	Description
mark_id	INT	Primary Key, IDENTITY(1,1)	Unique marks record ID
student_id	INT	Foreign Key	References students.student_id
subject_id	INT	Foreign Key	References subjects.subject_id
marks_obtained	INT	—	Marks obtained by the student


5. Database Relationships
The database uses the following relationships:
- students → marks: One student can have multiple marks records.
- subjects → marks: One subject can appear in multiple marks records.
- marks connects students and subjects through foreign keys.
       students                         subjects
   ┌────────────────┐               ┌────────────────┐
   │ PK student_id  │               │ PK subject_id  │
   │    student_name│               │    subject_name│
   │    email       │               │    total_marks │
   │    course      │               └────────┬───────┘
   │    admission_date                        │
   └────────┬───────┘                         │
            │                                 │
            │ 1                           1   │
            └───────────┐       ┌─────────────┘
                        ▼       ▼
                    ┌────────────────┐
                    │     marks      │
                    │ PK mark_id     │
                    │ FK student_id  │
                    │ FK subject_id  │
                    │    marks_obtained
                    └────────────────┘
This design allows a student to have marks in multiple subjects and a subject to have marks for multiple students.
6. Sample Data
The SQL script inserts:
- 3 students: Amit Patil, Priya Sharma, and Rahul Jadhav.
- 3 subjects: Chemistry, Mathematics, and Computer Science.
- 9 marks records: Three subject marks for each student.
The sample course is BSc Chemistry. Each subject has a maximum of 100 marks.
7. SQL Concepts and Operations Implemented
Database and table creation
- CREATE DATABASE
- USE
- CREATE TABLE
Constraints
- PRIMARY KEY
- FOREIGN KEY
- NOT NULL
- UNIQUE
- IDENTITY(1,1)
Data manipulation
- INSERT INTO
Data retrieval
- SELECT
- INNER JOIN
- GROUP BY
- ORDER BY
Aggregate and numeric functions
- AVG()
- ROUND()
Database objects
- VIEW
- STORED PROCEDURE
8. Important Queries
8.1 Display all students, subjects, and marks
Joins the three tables to display each student's subject-wise marks.
SELECT
    s.student_name,
    sub.subject_name,
    m.marks_obtained
FROM students s
INNER JOIN marks m
    ON s.student_id = m.student_id
INNER JOIN subjects sub
    ON m.subject_id = sub.subject_id;
8.2 Calculate average marks of each student
Uses AVG(), GROUP BY, and ORDER BY to calculate and rank average marks.
SELECT
    s.student_name,
    ROUND(AVG(m.marks_obtained), 2) AS average_marks
FROM students s
INNER JOIN marks m
    ON s.student_id = m.student_id
GROUP BY s.student_id, s.student_name
ORDER BY average_marks DESC;
9. View: student_performance
The project creates a view named student_performance. It displays each student's average marks.
CREATE VIEW student_performance AS
SELECT
    s.student_name,
    ROUND(AVG(m.marks_obtained), 2) AS average_marks
FROM students s
INNER JOIN marks m
    ON s.student_id = m.student_id
GROUP BY s.student_id, s.student_name;
To retrieve the view:
SELECT * FROM student_performance;
Purpose: A view provides a reusable way to access the average-performance query without writing the complete query every time.
10. Stored Procedure: GetStudentMarks
The project creates a parameterized stored procedure named GetStudentMarks.

It accepts a student ID and returns that student's name, subject names, and marks.
CREATE PROCEDURE GetStudentMarks
    @studentId INT
AS
BEGIN
    SELECT
        s.student_name,
        sub.subject_name,
        m.marks_obtained
    FROM students s
    INNER JOIN marks m
        ON s.student_id = m.student_id
    INNER JOIN subjects sub
        ON m.subject_id = sub.subject_id
    WHERE s.student_id = @studentId;
END;
GO
Execute the procedure:
EXEC GetStudentMarks @studentId = 1;
Purpose: The procedure makes it easy to retrieve marks for a particular student by passing their ID as a parameter.
11. How to Run the Project
1. Install Microsoft SQL Server.
2. Open SQL Server Management Studio (SSMS).
3. Connect to your SQL Server instance.
4. Open the file project_students_management.sql.
5. Execute the complete script.
6. Refresh the Databases section and confirm that student_management has been created.
7. Run the following queries to verify the data and objects:
USE student_management;

SELECT * FROM students;
SELECT * FROM subjects;
SELECT * FROM marks;

SELECT * FROM student_performance;

EXEC GetStudentMarks @studentId = 1;
Run the creation script against a fresh database, or remove the existing database objects before rerunning it. The current script does not include DROP or IF NOT EXISTS checks.

12. Current Project Scope
The uploaded SQL script implements:
Feature	Status
Database creation	Implemented
Three relational tables	Implemented
Primary and foreign keys	Implemented
Unique and NOT NULL constraints	Implemented
Sample data insertion	Implemented
INNER JOIN queries	Implemented
Average marks calculation	Implemented
View	Implemented
Stored procedure	Implemented
Triggers	Not included in uploaded script
Explicit index creation	Not included in uploaded script
UPDATE and DELETE operations	Not demonstrated in uploaded script


13. Future Enhancements
The project can be extended with:
- Triggers to maintain an audit log when marks are inserted or updated.
- Indexes to improve performance for frequently searched columns.
- UPDATE and DELETE operations for student and marks records.
- Input validation to prevent marks exceeding the subject's maximum marks.
- A rule to prevent duplicate marks entries for the same student and subject.
- Additional reports for subject-wise averages, highest marks, and pass/fail status.
- A front-end application for managing student records.
14. Learning Outcomes
Through this project, the following SQL Server concepts are demonstrated:
- Designing a relational database.
- Creating tables with keys and constraints.
- Establishing relationships using foreign keys.
- Retrieving data using joins.
- Performing calculations using aggregate functions.
- Creating reusable views.
- Developing and executing parameterized stored procedures.
Project: Student Management System
Database: student_management
Technology: Microsoft SQL Server (T-SQL)
Project Type: SQL Developer Portfolio Project
