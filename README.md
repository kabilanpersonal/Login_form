<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome</title>
    <link rel="stylesheet" href="assets/welcome.css">




    <script type="text/javascript" src="https://code.jquery.com/jquery-1.12.0.min.js"></script>
    <meta charset="utf-8">
      <meta name="viewport" content="width=device-width, initial-scale=1">

      <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/5.0.0-alpha1/css/bootstrap.min.css" rel="nofollow" integrity="sha384-r4NyP46KrjDleawBgD5tp8Y7UzmLA05oM1iAEQ17CSuDqnUK2+k9luXQOfXJCJ4I" crossorigin=”anonymous”>
      <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">


   
</head>
<body>
   

        <nav>
            <a href="#first"><i class="far fa-user-plus"></i>Add User</a>
            <a href="#second"><i class="fas fa-search"></i>Search User</a>
            <a href="#third"><i class="far fa-user-times"></i>Delete User</a>
            
            </nav>
            
            <div class= 'container'> 
            <section id= 'first'>
            
        

                <form class="frm" >
                <label for="project-id">Project ID:</label>
                <input type="text" id="Projectid" name="project-id" placeholder="Enter Project ID" required>
                
                <label for="project-name">Project Name:</label>
                <input type="text" id="Projectname" name="project-name" placeholder="Enter Project Name" required>
                
                <label for="total-members">Total Members:</label>
                <input type="text" id="Totalmembers" name="total-members" placeholder="Enter Total Members" required>
                
                <label for="start-date">Start Date:</label>
                <input type="text" id="Startdate" name="start-date" placeholder="Enter Start Date" required>
                
                <label for="end-date">End Date:</label>
                <input type="text" id="Enddate" name="end-date" placeholder="Enter End Date" required>
                
                <button type="button" onclick="add()" class="btn">Submit</button>
                <!-- <input type="submit" value="Submit" onclick="add()"> -->
                <input type="reset" value="Clear"><br>
                <h3 id="msg" style="color: red;"></h3> 
                </form>
                
                

            </section>
            
            <section id= 'second'>
                

                <form>
                <label for="search-query">Search User:</label>
                <input type="text" id="search-query" name="search-query" placeholder="Enter username or email" required>
                
                <button type="button" onclick="getData()">Search</button>
                </form>
                <br>
                <p id="searchresult"></p>
                <button type="button" class="btn"  href="javascript:history.go(-1)">Back</button>
                
            </section>
            
            <section id= 'third'>
              
                <form>
                <label for="search-query">Search User:</label>
                <input type="text" id="search-query" name="search-query" placeholder="Enter username or email" required>
                
                <input type="submit" value="Search" onclick="confirmDelete()">
                </form>
            </section>
            
            
            </div>

<script>
// Add User
        function add() {

            
            const Projectid = document.getElementById("Projectid").value;
            const Projectname = document.getElementById("Projectname").value;
            const Totalmembers = document.getElementById("Totalmembers").value;
            const Startdate= document.getElementById("Startdate").value;
            const Enddate = document.getElementById("Enddate").value;

if (Projectname && Projectid && Totalmembers && Startdate && Enddate ) {

    fetch('http://localhost:3001/add1', {

    method: 'POST',
    body: JSON.stringify({

      Projectid:Projectid,
      Projectname:Projectname, 
      Totalmembers:Totalmembers,
      Startdate:Startdate,
      Enddate:Enddate
       }),

    headers: {
      'Content-type': 'application/json; charset=UTF-8',
    }

    })
    .then(
      respose => respose.json()
    )
  .then(function(data){
    console.log("inside the function")
    console.log(data)

      if(data==true)
      {
        console.log("Inside the if condition")
         document.getElementById("msg").innerHTML="Data Added Successfully !!!";
      }else{
        document.getElementById("msg").innerHTML=data.message;
      }
  }).catch(error => {console.error('Error:', error.message);
  

});

  }
  else{
    alert("Please Fill all the fields")
  }
}

 </script>



<script>

// Search by name

   function getData(){
      const word = document.getElementById("search-query").value;
       const response=  fetch(`http://localhost:3001/getOne2:Projectname=${word}`).then(
    respose => respose.json()
)
.then(data => {
    console.log(data)
    if(data.length > 1){
        document.getElementById("searchresult").innerHTML=data;
      
    }
    else{
        window.location.href = "invalid.html";
    }
  })

    }

</script>
</body>
</html>
