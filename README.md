# Login2Explore-Micro-project-code

Title of the Project - Student Enrollment Form that will store data in STUDENT-TABLE relation of SCHOOL-DB database.

Description - Create a  Student Enrollment form. The form should store data in the database. The primary key and input fields of each topic is mentioned.

There will be three control buttons [Save], [Update] and [Reset] at the bottom of the form. On page load or any control button click, an empty form will be displayed and the cursor will remain at the first input field in the form which will have the primary key in the relation. All other fields and buttons should be disabled at this time.

User will enter data in the field having primary key and

If the primary key value does NOT exist in the database, enable [Save] and [Reset] buttons and move the cursor to the next field and allow the user to enter data in the form.

Check that the data should be valid i.e. no empty fields.

Complete the data entry form and click the [Save] button to store the data in the database and go to step-2.

If the primary key value is present in the database, display that data in the form. Enable [Update] and [Reset] buttons and move the cursor to the next' field in the form. Keep the primary key field disabled and allow users to change other form fields.

Check that the data should be valid i.e. no empty fields.

Click on [Update] button to update the data in the database and go to step-2.

Click [Reset] to reset the form as per the step-2.
Input Fields: {Roll-No, Full-Name, Class, Birth-Date, Address, Enrollment-Date}
Primary key: Roll No.

Benefits of using JsonPowerDB - * High Performance:
    * JsonPowerDB offers high-performance CRUD operations (Create, Read, Update, Delete) on JSON data. It is optimized for handling JSON documents efficiently.
    * The database engine is designed to deliver fast read and write operations, making it suitable for applications that require real-time data processing.

* Schema-free:
    * JsonPowerDB is schema-free, allowing you to store JSON data without predefined schemas. This flexibility simplifies the data modeling process and accommodates changes in data structures without requiring a schema modification.

* REST API:
    * JsonPowerDB provides a REST API interface, making it easy to integrate with web and mobile applications. HTTP methods such as GET, POST, PUT, and DELETE can be used to interact with the database, making it accessible from various programming languages.

* Multi-mode Database:
    * JsonPowerDB supports both single-mode and multi-mode, allowing it to function as both a document-oriented database and a key-value store. This versatility enables developers to choose the best data model for their specific use case.

* Real-time Replication:
    * JsonPowerDB supports real-time data replication, ensuring that changes made to the database are immediately reflected across all replicas. This feature enhances data consistency and fault tolerance.

* Built-in Analytics:
    * JsonPowerDB includes built-in analytical functions that enable users to perform data analysis directly within the database. This feature simplifies the process of extracting meaningful insights from large datasets.

* Low Development and Maintenance Costs:
    * JsonPowerDB's simplicity and ease of use reduce development time and effort. Its schema-free nature eliminates the need for complex schema designs and modifications, lowering development and maintenance costs.

* Agile Development:
    * JsonPowerDB supports agile development methodologies by allowing developers to quickly adapt to changing data requirements. Developers can easily modify data structures without disrupting existing applications.

* In-memory Database:
    * JsonPowerDB can function as an in-memory database, storing data in system memory rather than on disk. This results in faster read and write operations, making it ideal for applications requiring low latency.

* Community Support and Documentation:
    * JsonPowerDB benefits from an active community that provides support, tutorials, and documentation. Developers can find resources and assistance to help them effectively use the database for their projects.

release of JsonPowerDB related code - 

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Enrollment Form</title>
    <style>
        .form-container {
            max-width: 400px;
            margin: 0 auto;
            padding: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
        }

        .form-group input {
            width: 100%;
            padding: 8px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        .form-group button {
            background-color: #4caf50;
            color: white;
            border: none;
            padding: 10px 20px;
            cursor: pointer;
        }

        .form-group button:disabled {
            background-color: #ccc;
        }
    </style>
</head>

<body>
    <div class="form-container">
        <div class="form-group">
            <label for="rollNo">Roll No:</label>
            <input type="text" id="rollNo" disabled>
        </div>
        <div class="form-group">
            <label for="fullName">Full Name:</label>
            <input type="text" id="fullName" required>
        </div>
        <div class="form-group">
            <label for="class">Class:</label>
            <input type="text" id="class" required>
        </div>
        <div class="form-group">
            <label for="birthDate">Birth Date:</label>
            <input type="date" id="birthDate" required>
        </div>
        <div class="form-group">
            <label for="address">Address:</label>
            <input type="text" id="address" required>
        </div>
        <div class="form-group">
            <label for="enrollmentDate">Enrollment Date:</label>
            <input type="date" id="enrollmentDate" required>
        </div>
        <div class="form-group">
            <button id="saveBtn" disabled>Save</button>
            <button id="updateBtn" disabled>Update</button>
            <button id="resetBtn">Reset</button>
        </div>
    </div>

    <script>
        const rollNoInput = document.getElementById('rollNo');
        const fullNameInput = document.getElementById('fullName');
        const classInput = document.getElementById('class');
        const birthDateInput = document.getElementById('birthDate');
        const addressInput = document.getElementById('address');
        const enrollmentDateInput = document.getElementById('enrollmentDate');
        const saveBtn = document.getElementById('saveBtn');
        const updateBtn = document.getElementById('updateBtn');
        const resetBtn = document.getElementById('resetBtn');

        resetBtn.addEventListener('click', function () {
            clearForm();
        });

        function clearForm() {
            rollNoInput.value = '';
            fullNameInput.value = '';
            classInput.value = '';
            birthDateInput.value = '';
            addressInput.value = '';
            enrollmentDateInput.value = '';
            saveBtn.disabled = true;
            updateBtn.disabled = true;
        }

        clearForm(); // Call this function on page load

        // Add event listeners to input fields for validation
        fullNameInput.addEventListener('input', validateForm);
        classInput.addEventListener('input', validateForm);
        birthDateInput.addEventListener('input', validateForm);
        addressInput.addEventListener('input', validateForm);
        enrollmentDateInput.addEventListener('input', validateForm);

        function validateForm() {
            const isFormValid = fullNameInput.value.trim() !== '' &&
                classInput.value.trim() !== '' &&
                birthDateInput.value.trim() !== '' &&
                addressInput.value.trim() !== '' &&
                enrollmentDateInput.value.trim() !== '';

            saveBtn.disabled = !isFormValid;
            updateBtn.disabled = !isFormValid;
        }
    </script>
</body>

</html>

Serever Side Code - 

const express = require('express');
const bodyParser = require('body-parser');
const JsonPowerDB = require('jsonpowerdb');

const app = express();
app.use(bodyParser.urlencoded({ extended: true }));
app.use(bodyParser.json());

// Connect to JsonPowerDB (assuming JsonPowerDB server is running on http://localhost:7700/)
const jpdb = new JsonPowerDB('http://localhost:7700/');

app.post('/saveStudent', (req, res) => {
    const { rollNo, fullName, className, birthDate, address, enrollmentDate } = req.body;

    // Validate data (add your validation logic here)
    if (!rollNo || !fullName || !className || !birthDate || !address || !enrollmentDate) {
        return res.status(400).json({ error: 'All fields are required.' });
    }

    // Create a new record in JsonPowerDB
    const response = jpdb.insert('STUDENT_TABLE', {
        RollNo: rollNo,
        FullName: fullName,
        Class: className,
        BirthDate: birthDate,
        Address: address,
        EnrollmentDate: enrollmentDate
    });

    return res.json(response);
});

// Add more routes for updating, retrieving, and deleting records as needed

const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});








