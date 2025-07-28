<!DOCTYPE html> 
<html> 
<head> 
  <title>User Data Collection</title> 
</head> 
<body> 

<?php 
// MySQL database configuration 
$servername = "192.168.30.7"; 
$username = "udc123"; 
$password = "Root@123"; 
$dbname = "udc"; 

// Create database connection 
$conn = new mysqli($servername, $username, $password, $dbname); 

// Check connection 
if ($conn->connect_error) { 
  die("Connection failed: " . $conn->connect_error); 
} 

if ($_SERVER["REQUEST_METHOD"] == "POST") { 
  // Collect user data 
  $name = $_POST["name"]; 
  $age = $_POST["age"]; 
  $country = $_POST["country"]; 
  
  // Collect checkbox values (array)
  $degrees = isset($_POST['degree']) ? implode(", ", $_POST['degree']) : "";

  // Insert into database
  $sql = "INSERT INTO users (name, age, country, degree) VALUES ('$name', $age, '$country', '$degrees')"; 
  
  if ($conn->query($sql) === TRUE) { 
    echo "User data has been successfully stored in the database.<br>"; 
  } else { 
    echo "Error: " . $sql . "<br>" . $conn->error; 
  } 

  // Upload userfile
  $uploadDir = '/var/udc/uploads/'; 
  
  // Upload profile file
  $userfilePath = $uploadDir . basename($_FILES['userfile']['name']); 
  if (move_uploaded_file($_FILES['userfile']['tmp_name'], $userfilePath)) { 
    echo "Profile file uploaded successfully.<br>"; 
  } else { 
    echo "Profile file upload failed.<br>"; 
  }

  // Upload resume file
  $resumePath = $uploadDir . basename($_FILES['resume']['name']); 
  if (move_uploaded_file($_FILES['resume']['tmp_name'], $resumePath)) { 
    echo "Resume uploaded successfully.<br>"; 
  } else { 
    echo "Resume upload failed.<br>"; 
  }
} 
?> 

<h2>Enter User Information</h2> 
<form method="post" enctype="multipart/form-data"> 
  Name: <input type="text" name="name"><br> 
  Age: <input type="number" name="age"><br> 
  Country: <input type="text" name="country"><br>

  Degree:<br>
  <input type="checkbox" name="degree[]" value="B.E"> B.E<br>
  <input type="checkbox" name="degree[]" value="B.Tech"> B.Tech<br>
  <input type="checkbox" name="degree[]" value="M.E"> M.E<br>
  <input type="checkbox" name="degree[]" value="M.Tech"> M.Tech<br>

  Profile File Upload: <input type="file" name="userfile"><br> 
  Resume Upload: <input type="file" name="resume"><br> 

  <input type="submit" value="Submit"> 
</form> 

<?php 
// Close connection 
$conn->close(); 
?> 

</body> 
</html>
