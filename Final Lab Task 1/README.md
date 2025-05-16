# Final Lab Task 1: MYSQL Basics


## Step 1: Create the Employees Table
- Define employee_id as auto-incremented primary key
- Add employee_name as VARCHAR(255) and NOT NULL
- Add manager_id as a foreign key referencing employee_id in the same table
## Step 2: Create the Departments Table
- Define department_id as auto-incremented primary key
- Add department_name as VARCHAR(255) and NOT NULL
## Step 3: Create the employee_departments table
- Add employee_id referencing employees.employee_id
- Add department_id referencing departments.department_id
- Set a composite primary key on both
## Step 4: Create the employee_projects table
- Define employee_id as an integer, which will be a foreign key referencing employee_id in the employees table.
- Define project_name as a VARCHAR (up to 255 characters), and make it not null.
## Step 5: Create the managers table
- Define manager_id as a unique integer, auto-increment, and primary key.
- Define employee_id as an integer, which will be a foreign key referencing employee_id in the employees table.
# Query Statement

# Table Structure

# Entity-Relationship Schema
