### Hi there 👋

<!--
**PuneetNarwani/PuneetNarwani** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->


<?php
  if(isset($_POST['submit']))
  {
    $name=$_POST['name'];
	$phone=$_POST['phone'];
	$email=$_POST['email'];
	$other=$_POST['other'];
	$imagename=$_FILES['image']['name'];
	$tmp_name=$_FILES['image']['tmp_name'];
	$folder="trip/".$imagename;
	echo $name.$phone.$email.$other.$imagename ;
	
	// inserting from data in databse
	$con=mysqli_connect("localhost","root","","ustrip");
	$query="INSERT INTO `trip` (`name`, `phone`, `email`, `image`, `other`) VALUES ('$name', '$phone', '$email','$imagename', '$other')";
	mysqli_query($con,$query);
	//INSERT INTO `trip` (`Sno`, `name`, `phone`, `email`, `image`, `other`) VALUES ('1', 'puneet narwani', '123456789', 'puneet@gmail.com', 'Snapchat-482659758.jpg', 'i m puneet');
	
	//moving image to folder
  if (move_uploaded_file('$tmp_name','$folder'))  { 
            $msg = "Image uploaded successfully"; 
        }else{ 
            $msg = "Failed to upload image"; 
      }
	
  }
  if(isset($_GET['ShowData']))
  {
    // echo "Good Morning";
    $con=mysqli_connect("localhost","root","","ustrip");
	$query="select * from trip ";
	$run=mysqli_query($con,$query);
	
	while($res=mysqli_fetch_array($run))
	{
	  ?>
	  <table>
	    <tr>
		  <th>Sno</th>
		  <th>Name</th>
		  <th>Phone</th>
		  <th>E-mail</th>
		  <th>Image</th>
		  <th>Others</th>
		</tr>
	    <tr>
		  <td><?php echo $res['Sno']?></td>
		  <td><?php echo $res['name']?></td>
		  <td><?php echo $res['phone']?></td>
		  <td><?php echo $res['email']?></td>
		  <td><img src="trip/<?php echo $res['image']; ?>"></td>
		  <td><?php echo $res['other']?></td>
		</tr>
	  </table>
	  <?php
	}
  }
?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>US_Trip Form</title>
</head>
<body>
    <form action="" method="post" enctype="multipart/form-data" style="display:block; text-transform:capitalize; text-align:center;">
      <table align="center">
        <tr>
		  <td>NAME=></td>
		  <td><input type="text" name="name" placeholder="enter your name" required></td>
		</tr>
		<tr>
		  <td>Phone Number=></td>
		  <td><input type="text" name="phone" placeholder="enter your phone number" required></td>
		</tr>
		<tr>
		  <td>E-mail=></td>
		  <td><input type="email" name="email" placeholder="enter your E-mail" required></td>
		</tr>
		<tr>
		  <td>Upload Image=></td>
		  <td><input type="file" name="image" required></td>
		</tr>
		<tr>
		  <td>Other Information=></td>
		  <td><textarea name="other" cols="6" rows="10"></textarea></td>
		</tr>
		<tr>
		  <td><input type="submit" name="submit"></td>
		  <td><input type="reset" name="reset"></td>
		</tr>
      </table>
    </form>
	<form method="get" action="">
	<table>
	<tr align="center">
		  <td align="center">
		   <input align="middle" type="submit" name="ShowData" value="show data">
		   </td>
		</tr>
	</table>
	</form>
</body>
</html>
