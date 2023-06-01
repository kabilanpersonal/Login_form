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
    else if (results.length == 0) {

      res.status(404).json({ error: 'Invalid Credentials' });

    } 
    else {

        res.json({ message: 'Login successful' });

    }

  });

});

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Validation</title>
    <link rel="stylesheet" href="assets/style.css">
</head>
<body>
    <section class="box">
        <div class="design">
            <div></div>
            <div></div>
            <div></div>
            <div></div>
        </div>
        <div class="form">
            <h2>User Login</h2>
            <form action="/" method="POST">
                <input type="email" name="username" class="input-field" placeholder="Username" required/>
                <input type="password" name="password" class="input-field" placeholder="Password" required/>
                <input type="submit" class="btn" value="LOGIN">
            </form>
        </div>
    </section>
</body>
</html>


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>User Validation</title>
    <link rel="stylesheet" href="assets/style.css">
</head>
<body>
    <section class="box">
        <div class="design">
            <div></div>
            <div></div>
            <div></div>
            <div></div>
        </div>
        <div class="form">
            <h2>User Login</h2>
            <form action="/" method="POST">
                <input type="email" name="username" class="input-field" placeholder="Username" required/>
                <input type="password" name="password" class="input-field" placeholder="Password" required/>
                <input type="submit" class="btn" value="LOGIN">
            </form>
        </div>
    </section>
</body>
</html>

const mysql = require("mysql2");
const express = require("express");
const bodyParser = require("body-parser");
const encoder = bodyParser.urlencoded();

const app = express();
app.use(express.json());
app.use(express.urlencoded({
    extended: true
}));

app.use("/assets",express.static("assets"));

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


app.get("/",function(req,res){
    res.sendFile(__dirname + "/index.html");
})

app.post("/",encoder, function(req,res){
    var username = req.body.username;
    var password = req.body.password;
    console.log(username,password);
    //var username="admin2@gmail.com";
    //var password="Admin@123";

    connection.query("SELECT * FROM login where Username = ? and Password = ?",[username,password],function(error,results,fields){
        console.log(results);
        if (results.length > 0) {
            res.redirect("/welcome");
        } else {
            res.redirect("/invalid");
        }
        res.end();
    })
})

// when login is success
app.get("/welcome",function(req,res){
    res.sendFile(__dirname + "/welcome.html")

})

// when login is fail
app.get("/invalid",function(req,res){
    res.sendFile(__dirname + "/invalid.html")
})


// set app port 
app.listen(4500);
