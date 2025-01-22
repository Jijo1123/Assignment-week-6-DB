-- Question 1: Bills and Payments Table Join (INNER JOIN)
SELECT 
    b.TotalAmount, 
    b.Status, 
    p.DueDate, 
    p.PaymentMethod, 
    p.PaymentAmount
FROM bills b
INNER JOIN payments p ON b.BillID = p.BillID;

-- Question 2: Customer and Bills Table Join (LEFT JOIN)
SELECT 
    c.customerName, 
    c.email, 
    c.customerAddress, 
    b.TotalAmount, 
    b.Status
FROM customer c
LEFT JOIN bills b ON c.CustomerID = b.CustomerID;

-- Question 3: Bills and Bill Items Table Join (RIGHT JOIN)
SELECT 
    b.BillDate, 
    b.DueDate, 
    bi.Status, 
    bi.ItemDescription, 
    bi.Quantity, 
    bi.LineTotal,
    DATEDIFF(b.DueDate, b.BillDate) AS Number_of_Days
FROM bills b
RIGHT JOIN bill_items bi ON b.BillID = bi.BillID;

-- Question 4: One-to-One Relationship: Users and User Profiles
-- Create users table
CREATE TABLE users (
    user_id INT PRIMARY KEY,
    username VARCHAR(100) NOT NULL
);

-- Create user_profiles table with foreign key constraint for one-to-one relationship
CREATE TABLE user_profiles (
    profile_id INT PRIMARY KEY,
    user_id INT UNIQUE,  -- Ensure a one-to-one relationship
    profile_data TEXT,
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);

-- Question 5: One-to-Many Relationship: Departments and Employees
-- Create departments table
CREATE TABLE departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL
);

-- Create employees table with foreign key referencing departments table
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    employee_name VARCHAR(100) NOT NULL,
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(department_id)
);

-- Question 6: Categories, Bills, and Customer Tables Join (INNER JOIN & LEFT JOIN)
SELECT 
    c.CategoryName, 
    b.TotalAmount, 
    b.DueDate, 
    cu.customerName, 
    cu.customerAddress
FROM categories c
INNER JOIN bills b ON c.CategoryID = b.CategoryID
LEFT JOIN customer cu ON b.CustomerID = cu.CustomerID;
