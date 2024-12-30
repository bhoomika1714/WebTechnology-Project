```
const express = require('express');
const mysql = require('mysql');
const bodyParser = require('body-parser');

const app = express();
const port = 3000;

const db = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: '',
    database: 'exam_registration'
});

db.connect((err) => {
    if (err) {
        console.error('Error connecting to database: ' + err.stack);
        return;
    }
    console.log('Connected to database!');
});

app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static('public'));

app.get('/', (req, res) => {
   
    db.query('SELECT exam_type, COUNT(*) as total FROM registrations GROUP BY exam_type', (err, result) => {
        if (err) throw err;

        const examCounts = {
            bank: 0,
            railway: 0,
            ksrtc: 0
        };

    
        result.forEach(row => {
            examCounts[row.exam_type] = row.total;
        });

        res.send(`
            <head>
                <link rel="stylesheet" href="/styles.css">
            </head>

            <h1>Welcome to the Entrance Exam Registration</h1>
            <nav>
                <ul>
                    <li><a href="/bank-exams">Bank Exams</a> (Total Registrations: ${examCounts.bank})</li>
                    <li><a href="/railway-exams">Railway Exams</a> (Total Registrations: ${examCounts.railway})</li>
                    <li><a href="/ksrtc-exams">KSRTC Exams</a> (Total Registrations: ${examCounts.ksrtc})</li>
                    <li><a href="/user-services">User Services</a></li>
                </ul>
            </nav>
            
           
            <p align="center" >REGISTER NOW!!!!</p>
        `);
    });
});


app.get('/bank-exams', (req, res) => {
    res.send(`
        <head>
            <link rel="stylesheet" href="/styles.css">
        </head>

        <h1>Bank Exams Registration</h1>
        <form action="/register-bank" method="POST">
            <label for="name">Name:</label><br>
            <input type="text" id="name" name="name" required><br>
            <label for="age">Age:</label><br>
            <input type="number" id="age" name="age" required><br>
            <label for="marks">Marks:</label><br>
            <input type="number" id="marks" name="marks" required><br>
            <label for="qualification">Qualifications:</label><br>
            <input type="text" id="qualification" name="qualification" required><br>
            <label for="contact">Contact Number:</label><br>
            <input type="text" id="contact" name="contact" required><br>
            <label for="email">Email ID:</label><br>
            <input type="email" id="email" name="email" required><br>
            <label for="address">Address:</label><br>
            <textarea id="address" name="address" required></textarea><br><br>
            <input type="submit" value="Register">
        </form>
    `);
});


app.get('/railway-exams', (req, res) => {
    res.send(`
        <head>
            <link rel="stylesheet" href="/styles.css">
        </head>

        <h1>Railway Exams Registration</h1>
        <form action="/register-railway" method="POST">
            <label for="name">Name:</label><br>
            <input type="text" id="name" name="name" required><br>
            <label for="age">Age:</label><br>
            <input type="number" id="age" name="age" required><br>
            <label for="marks">Marks:</label><br>
            <input type="number" id="marks" name="marks" required><br>
            <label for="qualification">Qualifications:</label><br>
            <input type="text" id="qualification" name="qualification" required><br>
            <label for="contact">Contact Number:</label><br>
            <input type="text" id="contact" name="contact" required><br>
            <label for="email">Email ID:</label><br>
            <input type="email" id="email" name="email" required><br>
            <label for="address">Address:</label><br>
            <textarea id="address" name="address" required></textarea><br><br>
            <input type="submit" value="Register">
        </form>
    `);
});


app.get('/ksrtc-exams', (req, res) => {
    res.send(`
        <head>
            <link rel="stylesheet" href="/styles.css">
        </head>

        <h1>KSRTC Exams Registration</h1>
        <form action="/register-ksrtc" method="POST">
            <label for="name">Name:</label><br>
            <input type="text" id="name" name="name" required><br>
            <label for="age">Age:</label><br>
            <input type="number" id="age" name="age" required><br>
            <label for="marks">Marks:</label><br>
            <input type="number" id="marks" name="marks" required><br>
            <label for="qualification">Qualifications:</label><br>
            <input type="text" id="qualification" name="qualification" required><br>
            <label for="contact">Contact Number:</label><br>
            <input type="text" id="contact" name="contact" required><br>
            <label for="email">Email ID:</label><br>
            <input type="email" id="email" name="email" required><br>
            <label for="address">Address:</label><br>
            <textarea id="address" name="address" required></textarea><br><br>
            <input type="submit" value="Register">
        </form>
    `);
});


app.get('/user-services', (req, res) => {
    res.send(`
        <head>
            <link rel="stylesheet" href="/styles.css">
        </head>

        <h1>Shortlisted Students</h1>
        <ul>
            <li><a href="/shortlist-bank-exams">Bank Exams Shortlist</a></li>
            <li><a href="/shortlist-railway-exams">Railway Exams Shortlist</a></li>
            <li><a href="/shortlist-ksrtc-exams">KSRTC Exams Shortlist</a></li>
        </ul>
    `);
});


app.get('/shortlist-bank-exams', (req, res) => {
    db.query('SELECT * FROM registrations WHERE exam_type="bank" AND marks >= 90', (err, result) => {
        if (err) throw err;
        res.send(`
            <h1>Shortlisted Students for Bank Exams</h1>
            <ul>
                ${result.map(student => `<li>${student.name} - ${student.marks}%</li>`).join('')}
            </ul>
        `);
    });
});


app.get('/shortlist-railway-exams', (req, res) => {
    db.query('SELECT * FROM registrations WHERE exam_type="railway" AND marks >= 80', (err, result) => {
        if (err) throw err;
        res.send(`
            <h1>Shortlisted Students for Railway Exams</h1>
            <ul>
                ${result.map(student => `<li>${student.name} - ${student.marks}%</li>`).join('')}
            </ul>
        `);
    });
});


app.get('/shortlist-ksrtc-exams', (req, res) => {
    db.query('SELECT * FROM registrations WHERE exam_type="ksrtc" AND marks >= 75', (err, result) => {
        if (err) throw err;
        res.send(`
            <h1>Shortlisted Students for KSRTC Exams</h1>
            <ul>
                ${result.map(student => `<li>${student.name} - ${student.marks}%</li>`).join('')}
            </ul>
        `);
    });
});


app.post('/register-bank', (req, res) => {
    const { name, age, marks, qualification, contact, email, address } = req.body;
    const registrationNumber = `BANK-${Date.now()}`;
    const examType = 'bank';

    const query = 'INSERT INTO registrations (name, age, marks, qualification, contact, email, address, registration_number, exam_type) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)';
    db.query(query, [name, age, marks, qualification, contact, email, address, registrationNumber, examType], (err, result) => {
        if (err) throw err;
        res.send(`Registration successful! Your registration number is ${registrationNumber}`);
    });
});


app.post('/register-railway', (req, res) => {
    const { name, age, marks, qualification, contact, email, address } = req.body;
    const registrationNumber = `RAILWAY-${Date.now()}`;
    const examType = 'railway';

    const query = 'INSERT INTO registrations (name, age, marks, qualification, contact, email, address, registration_number, exam_type) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)';
    db.query(query, [name, age, marks, qualification, contact, email, address, registrationNumber, examType], (err, result) => {
        if (err) throw err;
        res.send(`Registration successful! Your registration number is ${registrationNumber}`);
    });
});


app.post('/register-ksrtc', (req, res) => {
    const { name, age, marks, qualification, contact, email, address } = req.body;
    const registrationNumber = `KSRTC-${Date.now()}`;
    const examType = 'ksrtc';

    const query = 'INSERT INTO registrations (name, age, marks, qualification, contact, email, address, registration_number, exam_type) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?)';
    db.query(query, [name, age, marks, qualification, contact, email, address, registrationNumber, examType], (err, result) => {
        if (err) throw err;
        res.send(`Registration successful! Your registration number is ${registrationNumber}`);
    });
});

app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});


// CREATE DATABASE exam_registration;

// USE exam_registration;

// CREATE TABLE registrations (
//     id INT AUTO_INCREMENT PRIMARY KEY,
//     name VARCHAR(100),
//     age INT,
//     marks INT,
//     qualification VARCHAR(100),
//     contact VARCHAR(15),
//     email VARCHAR(100),
//     address TEXT,
//     registration_number VARCHAR(50) UNIQUE,
//     exam_type ENUM('bank', 'railway', 'ksrtc') 
// );
// INSERT INTO registrations (name, age, marks, qualification, contact, email, address, registration_number, exam_type) 
// VALUES
//     ('Rahul Sharma', 28, 85, 'B.Tech', '9876543210', 'rahul.sharma@email.com', '1234, MG Road, Bangalore, Karnataka', 'R1234567890', 'bank'),
//     ('Priya Verma', 25, 90, 'M.Sc', '9123456789', 'priya.verma@email.com', '5678, Sarjapur Road, Bangalore, Karnataka', 'P0987654321', 'railway'),
//     ('Anil Kumar', 30, 78, 'BA', '9876012345', 'anil.kumar@email.com', '9/3, New Delhi Street, New Delhi', 'A4567890123', 'ksrtc'),
//     ('Sneha Reddy', 24, 92, 'M.Tech', '9456781234', 'sneha.reddy@email.com', '4321, Banjara Hills, Hyderabad, Telangana', 'S1237894560', 'bank'),
//     ('Vishal Gupta', 35, 80, 'MBA', '9654321876', 'vishal.gupta@email.com', '101, Sector 15, Noida, Uttar Pradesh', 'V5678901234', 'railway'),
//     ('Ayesha Khan', 27, 88, 'B.Com', '9345678901', 'ayesha.khan@email.com', '7/15, Shivaji Nagar, Pune, Maharashtra', 'A2345678901', 'ksrtc'),
//     ('Ravi Mehta', 29, 70, 'MCA', '9178765432', 'ravi.mehta@email.com', '98, Kotturpuram, Chennai, Tamil Nadu', 'R3456789012', 'bank'),
//     ('Simran Arora', 22, 95, 'BCA', '9023456789', 'simran.arora@email.com', '56, MG Road, Chandigarh', 'S8901234567', 'railway'),
//     ('Vikram Patel', 31, 77, 'B.Com', '9001234567', 'vikram.patel@email.com', '12/45, Ashok Vihar, Delhi', 'V0123456789', 'ksrtc'),
//     ('Deepika Singh', 26, 84, 'BDS', '9823764510', 'deepika.singh@email.com', '28, Colaba, Mumbai, Maharashtra', 'D2345678901', 'bank');
// INSER INTO registrations(name,age,marks,qualification,contaxt)
```
