<!-- Code php start -->
<?php 
        // This seesion start
        session_start();
        // This include file for user
        include("conection/dbcon.php");
        include("conection/function.php");
        // Use this for check method
        if($_SERVER['REQUEST_METHOD'] == "POST") {
            // something was post
            $user_name = $_POST['user_name'];
            $password = $_POST['password'];
            

            // use statement
            if(!empty($user_name) && !empty($password) && !is_numeric($user_name)) {
                // read from  database
                $query = "select * from tbl_user where user_name = '$user_name' limit 1";
                $result = mysqli_query($conn, $query);
                // check result
                if($result){
                    if($result && mysqli_num_rows($result) > 0) {
                        // use this for get data result
                        $user_data = mysqli_fetch_assoc($result);
                        // check user data
                        if($user_data['password'] === $password) {
                            // check session user_id
                            $_SESSION['user_id'] = $user_data['user_id'];
                            // make this for show toastmessage
                            $_SESSION['toastMsg'] = "login Successfully!";
                            header("Location: index.php");
                            die;
                        }
                    }
                }
                // use this for show message when user login
                //echo "Wrong password!";
               
            }else{
                //echo "Please enter some valid information";
            }
        }


?>
<!-- Code php end -->

<!-- Code html start -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>login</title>
    <link rel="stylesheet" href="style1.css">
    <link href='https://unpkg.com/boxicons@2.1.4/css/boxicons.min.css' rel='stylesheet'>
    <link  href="https://fonts.googleapis.com/css2?family=lost:wght@500&display=swap" rel="stylesheet">
</head>
<body>
        <div class="main">
            <input type="checkbox" id="chk" aria-hidden="true">
            <div class="login">
                <form method="post">

                        <label for="chk" aria-hidden="true">login</label>
                        <input type="text" name="user_name" placeholder="User Name" require="">
                        <input type="password" name="password" placeholder="Password" require="">
                        <button type="submit"  value="login">login</button>

                        <!-- onclick="callAlert('You login successfully!')" -->
                        <!-- Make this script for show alert message -->
                         <!--<script src="message.js"></script>
                         <script>
                                function callAlert(msg) {
                                    alert(msg, 3000)
                                }
                         </script> -->

                         <div>
                                <a href="signup.php">Go to signup</a>
                         </div>
                        
                </form>
            </div>
        </div>
</body>
</html>
<!-- Code html end -->
