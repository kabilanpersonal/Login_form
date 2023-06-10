

<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
   
    <link rel="stylesheet" href="assets/side.css">
    
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.12.1/css/all.min.css">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.min.js" charset="utf-8"></script>
   
  </head>
  <body>

    <input type="checkbox" id="check">
    <!--header area start-->
    <header>
      <label for="check">
        <i class="fas fa-bars" id="sidebar_btn"></i>
      </label>
      <div class="left_area">
        <h3>Project<span>Details</span></h3>
      </div>
      <div class="right_area">
        <a href="index.html" class="logout_btn">Logout</a>
      </div>
    </header>
    <!--header area end-->
    <!--mobile navigation bar start-->
    <div class="mobile_nav">
      <div class="nav_bar">
       
        <i class="fa fa-bars nav_btn"></i>
      </div>
      <div class="mobile_nav_items">
        <a href="add.html"><i class="fas fa-plus"></i><span>Add Project Details</span></a>
        <a href="retrieve.html"><i class="fas fa-search"></i><span>Retrieve Project Details</span></a>
        <a href="delete.html"><i class="fas fa-trash"></i><span>Delete Project Details</span></a>
      </div>
    </div>
    <!--mobile navigation bar end-->
    <!--sidebar start-->
    <div class="sidebar">
      <div class="profile_info">
        <h4>Menu</h4>
       
      </div>
      <a href="add.html"><i class="fas fa-plus"></i><span>Add Project Details</span></a>
      <a href="retrieve.html"><i class="fas fa-search"></i><span>Retrieve Project Details</span></a>
      <a href="delete.html"><i class="fas fa-trash"></i><span>Delete Project Details</span></a>
     
    </div>
    
    <!--sidebar end-->
    <div class="content">
        
     <input id="input" type="text" placeholder="Name" autofocus> </input>
     <div id="display-data"></div>
      
<!-- <div id="data"></div>
<input type="text"id="search"> -->
          </div>
          
          <br>
          <br>
          <br>

          
          
    <script type="text/javascript">
    $(document).ready(function(){ 
        // toggle button 
      $('.nav_btn').click(function(){
        $('.mobile_nav_items').toggleClass('active');
      });
    });  // Back button disable
    // window.history.forward();
    //     function noBack() {
    //         window.history.forward();
    //     }

    //
    const apiEndpoint = "http://localhost:3001/getOne2/Projectname";
    const display = document.querySelector("#display-data");
    const input = document.querySelector("#input");

    const getData = async () => {
      const res = await fetch(apiEndpoint);
      const data = await res.json();
      return data
    }

    const displayUsers = async () =>
    {
      let query = input.value;
      console.log("Query::", query);
    
    const payload = await getData();
  
  let dataDisplay = payload.filter((eventData) => {
    if (query === ""){return eventData}
    else if (eventData.project_name.toLowerCase().includes(query.toLowerCase()))
    {
      return eventData
    }
  }).map((object) => {
    const {project_name, project_id, total_team_members, start_date, end_date } = object;
    return `
    <div class="container">
      <p>Project Name: ${project_name}</p>
      <p>Project ID: ${project_id}</p>
      <p>Total Team Members: ${total_team_members}</p>
      <p>Start Date: ${start_date}</p>
      <p>End Date: ${end_date}</p>
      </div>
      <hr>
      `

  }).join("");
  display.innerHTML = dataDisplay;
  }
  displayUsers();

  input.addEventListener("input", () =>{
    displayUsers();
  });

// fetch(`http://localhost:3001/fetchproject`)
</script>

  </body>
</html>
