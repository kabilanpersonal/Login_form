
const mysql = require("mysql2");
const express = require('express');
const bodyParser = require("body-parser");
const encoder = bodyParser.urlencoded();
const dotenv = require("dotenv");

const app = express();
app.use(express.json());
app.use(express.urlencoded({
    extended: true
}));

const connection = mysql.createConnection({
    host: "localhost",
    user: "root",
    password: "root",
    database: "Login"
});

// connect to the database
connection.connect(function(error){
    if (error) throw error
    else console.log("connected to the database successfully!")
});

const port =process.env.PORT || 3000;
app.listen(port, () =>{
    console.log(`Server running on port ${port}`);
});

// Entire Database 

app.get('/api/login', (req, res) => {
    const query = 'SELECT * FROM login' ;
    connection.query(query, (err, rows) => {
    if (err) {
    console.error('Error executing query:', err);
    res.status(500).json({ error: 'Failed to fetch users' });
    } else {
    res.json(rows);
    }
    });
    });

// Validate

app.get('/api/validate', (req, res) => {

const { Username, Password } = req.query;
const query = 'SELECT * FROM login WHERE Username = ? AND Password = ?';
connection.query(query, [Username,Password], (err, results) => {

    if (err) {

      console.error('Error executing query:', err);

      res.status(500).json({ error: 'Internal Server Error' });

    } 
    else if (results.length > 0) {

      return true;

    } 
    else {
        return false;
    }

  });

});

html file

<!DOCTYPE html>
<html>
<head>
<title>Login</title>
</head>
<body>
<h1>Login</h1>
<form action="http://localhost:3000/api/validate?Username=?&&Password=?" method="get">
<input type="text" name="Username" placeholder="Username" required>
<input type="password" name="Password" placeholder="Password"required>
<input type="submit" value="Login">
</form>

</body>
</html>

<!DOCTYPE html>
<html>
<head>
<title>Login</title>
</head>
<body>
<h1>Login</h1>
<form action="http://localhost:3000/api/validate?Username=?&&Password=?" method="get">
<input type="text" name="Username" placeholder="Username" required>
<input type="password" name="Password" placeholder="Password"required>
<input type="submit" value="Login">
</form>

</body>
</html>
