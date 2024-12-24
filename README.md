
Database Application Report: Student Management System
Introduction:
The Student Management System is a lightweight web-based application that manages student information using SQLite as the backend database. The frontend is built with HTML, CSS, and JavaScript, offering a simple interface to perform basic operations such as adding and viewing student records. This project is ideal for beginners looking to understand the integration of databases in web development.
Objective
The primary objective is to create an intuitive system for managing student information. The goals include:
Using SQLite for a standalone and lightweight database solution.
Designing a user-friendly interface with HTML and CSS.
Implementing data manipulation and interaction through JavaScript.
System Architecture
1. Frontend:
HTML: Structures the content and forms the user interface.
CSS: Adds styling to ensure the interface is visually appealing and easy to navigate.
JavaScript: Provides interactivity, processes user inputs, and interacts with the database.
2. Backend:
SQLite: Acts as the database engine, storing and managing student records efficiently without requiring a separate server.
Features
Add Student Records: A form allows users to input student details like name, age, and city.
View Records: Displays all stored student data in a tabular format.
No External Dependencies: Fully functional with basic tools, ensuring easy setup.



Database Design
Table: Students
		
Column	Type	Description
id	INTEGER	Auto-incremented unique identifier
name	TEXT	Full name of the student
age	INTEGER	Age of the student
city	TEXT	City of residence

Sample Data
ID	Name	Age	City
1	Ahmed Khan	20	Karachi
2	Fatima Ali	22	Lahore
3	Ayesha Siddiqui	19	Islamabad
4	Bilal Ahmed	21	Quetta
			

Code Implementation
Frontend (HTML and CSS)
html
Copy code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Management System</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f9f9f9;
            margin: 0;
            padding: 20px;
        }
        h1 {
            color: #333;
        }
        form {
            margin-bottom: 20px;
        }
        label {
            display: inline-block;
            width: 100px;
            margin-bottom: 10px;
        }
        input {
            padding: 8px;
            margin-bottom: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            width: calc(100% - 120px);
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
    </style>
</head>
<body>
    <h1>Student Management System</h1>
    <form id="student-form">
        <label for="name">Name:</label>
        <input type="text" id="name" placeholder="Enter full name" required><br>
        <label for="age">Age:</label>
        <input type="number" id="age" placeholder="Enter age" required><br>
        <label for="city">City:</label>
        <input type="text" id="city" placeholder="Enter city" required><br>
        <button type="button" onclick="addStudent()">Add Student</button>
    </form>
    <h2>Student List</h2>
    <table id="student-table">
        <thead>
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Age</th>
                <th>City</th>
            </tr>
        </thead>
        <tbody></tbody>
    </table>
    <script src="script.js"></script>
</body>
</html>
Frontend Logic (JavaScript)
javascript
Copy code
// Initialize SQLite database
const db = new SQL.Database();

// Create Students table
db.run(`
    CREATE TABLE IF NOT EXISTS Students (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        age INTEGER NOT NULL,
        city TEXT NOT NULL
    );
`);

// Add a student to the database
function addStudent() {
    const name = document.getElementById('name').value.trim();
    const age = parseInt(document.getElementById('age').value, 10);
    const city = document.getElementById('city').value.trim();

    if (name && age && city) {
        db.run(INSERT INTO Students (name, age, city) VALUES (?, ?, ?), [name, age, city]);
        loadStudents(); // Refresh student list
        document.getElementById('student-form').reset(); // Clear the form
    }
}

// Load all students from the database
function loadStudents() {
    const result = db.exec("SELECT * FROM Students");
    const tableBody = document.querySelector('#student-table tbody');
    tableBody.innerHTML = ''; // Clear previous rows

    if (result[0]) {
        result[0].values.forEach(row => {
            const tr = document.createElement('tr');
            row.forEach(cell => {
                const td = document.createElement('td');
                td.textContent = cell;
                tr.appendChild(td);
            });
            tableBody.appendChild(tr);
        });
    }
}

// Initial load
loadStudents();
Conclusion
This project highlights the simplicity and effectiveness of combining SQLite with basic web technologies. It offers a user-friendly platform for managing student data and demonstrates foundational concepts in web-based database applications.


Syed Adnan Mansoor
BSCS-2y-F-1
500938
