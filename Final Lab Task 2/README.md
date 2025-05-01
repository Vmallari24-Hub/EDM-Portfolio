# Final Lab Task 2: Transforming ER into Relational Tables
## Creation of the student Table
- Define the attribute username as VARCHAR(50)
- Designate username as the Primary Key to ensure uniqueness for each student record
## Creation of the assignment Table
- Define shortname as VARCHAR(50) and assign it as the Primary Key
- Define due_date as a DATE and specify it as NOT NULL to ensure all assignments have a deadline
- Define url as VARCHAR(255) and allow it to be NULL, accommodating optional resource links
## Creation of the submission Table
- Define username and shortname both as VARCHAR(50) to establish identifiers
- Define version as an INT to represent submission iterations
- Define submit_date as a DATE with a NOT NULL constraint
- Define data as TEXT to store the content of each submission
- Establish a Composite Primary Key composed of (username, shortname, version)
- Add Foreign Key constraints on username and shortname
## RELATIONSHIPS
- Many-to-One with student: Each submission belongs to one student
- Many-to-One with assignment: Each submission is for one assignment
- This models a Many-to-Many relationship between students and assignments, with version tracking multiple submissions
# Query Statements
![image alt](https://github.com/Vmallari24-Hub/EDM-Portfolio/blob/95ee2322111349501f23c93a11d7b963f9512b98/IMAGE/Cleaned%20and%20Normalized.png)
# Table Structures
# Relational Tables
