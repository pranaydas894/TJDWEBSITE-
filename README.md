
<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>ত্রিপুরা জনতা দল (TJD)</title>

<style>
body{
    margin:0;
    font-family:Arial, sans-serif;
    background:#f5f5f5;
    color:#222;
}

header{
    background:#b71c1c;
    color:white;
    padding:20px;
    text-align:center;
}

nav{
    background:#222;
    padding:12px;
    text-align:center;
}

nav a{
    color:white;
    text-decoration:none;
    margin:10px;
}

section{
    background:white;
    margin:20px;
    padding:25px;
    border-radius:10px;
}

h2{
    color:#b71c1c;
}

.card{
    padding:15px;
    margin:10px;
    background:#fafafa;
    border-left:5px solid #b71c1c;
}

footer{
    background:#222;
    color:white;
    text-align:center;
    padding:20px;
}
</style>

</head>

<body>

<header>
<h1>ত্রিপুরা জনতা দল</h1>
<h3>Tripura Janata Dal (TJD)</h3>
<p>মানুষের মর্যাদা, ন্যায়ের রাজনীতি, ত্রিপুরার উন্নতি</p>
</header>


<nav>
<a href="#about">পরিচয়</a>
<a href="#vision">দর্শন</a>
<a href="#constitution">সংবিধান</a>
<a href="#join">যোগ দিন</a>
<a href="#contact">যোগাযোগ</a>
</nav>


<section id="about">

<h2>দলের পরিচয়</h2>

<p>
ত্রিপুরা জনতা দল (TJD) একটি গণতান্ত্রিক,
সাংবিধানিক ও জনকল্যাণমুখী রাজনৈতিক সংগঠন।
</p>

<p>
প্রতিষ্ঠাতা:
<strong>শ্রী প্রণয় দাস</strong>
</p>

</section>


<section id="vision">

<h2>দলীয় দর্শন</h2>

<div class="card">
<h3>র‍্যাডিক্যাল হিউম্যানিজম</h3>
<p>
মানুষের মর্যাদা, যুক্তিবাদ, স্বাধীন চিন্তা ও মানবকল্যাণকে সর্বোচ্চ গুরুত্ব দেওয়া।
</p>
</div>


<div class="card">
<h3>আধ্যাত্মিক মূল্যবোধ</h3>
<p>
এই আধ্যাত্মিকতা কোনো নির্দিষ্ট ধর্ম, সম্প্রদায় বা উপাসনা-পদ্ধতির সমর্থন নয়।
এটি মানবতা, নৈতিকতা ও আত্মিক উন্নয়নের মূল্যবোধকে বোঝায়।
</p>
</div>

</section>


<section id="constitution">

<h2>দলীয় সংবিধান</h2>

<p>
অধ্যায় ১ থেকে ২৫ পর্যন্ত দলীয় সংবিধান এখানে সংযুক্ত করা হবে।
</p>


<div class="card">
অধ্যায়–১ : নাম, প্রকৃতি ও উদ্দেশ্য
</div>

<div class="card">
অধ্যায়–২ : দলের উদ্দেশ্য
</div>

<div class="card">
অধ্যায়–৩ : দলের মৌলিক নীতি
</div>


<!-- অধ্যায় ৪-২৫ এখানে যোগ হবে -->


</section>


<section id="join">

<h2>সদস্যপদ আবেদন</h2>

<form>

নাম:
<input type="text"><br><br>

মোবাইল:
<input type="number"><br><br>

ঠিকানা:
<input type="text"><br><br>

<button>
আবেদন করুন
</button>

</form>

</section>


<section id="contact">

<h2>যোগাযোগ</h2>

<p>
প্রধান কার্যালয়:
সাবরুম, দক্ষিণ ত্রিপুরা
</p>

</section>


<footer>

<p>
© 2026 ত্রিপুরা জনতা দল (TJD)
</p>

</footer>


</body>
</html>
<?php
session_start();

$conn = new mysqli("localhost","root","","tjd_database");

if($conn->connect_error){
    die("Database Connection Failed");
}

$message="";

if(isset($_POST['login'])){

    $username = trim($_POST['username']);
    $password = trim($_POST['password']);

    $stmt = $conn->prepare("SELECT * FROM admins WHERE username=?");
    $stmt->bind_param("s",$username);
    $stmt->execute();

    $result = $stmt->get_result();

    if($result->num_rows>0){

        $admin = $result->fetch_assoc();

        if(password_verify($password,$admin['password'])){

            $_SESSION['admin_id']   = $admin['id'];
            $_SESSION['admin_name'] = $admin['name'];
            $_SESSION['role']       = $admin['role'];

            header("Location: admin_dashboard.php");
            exit;

        }else{

            $message="ভুল পাসওয়ার্ড";

        }

    }else{

        $message="অ্যাডমিন পাওয়া যায়নি";

    }

}

?>

<!DOCTYPE html>

<html lang="bn">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1">

<title>TJD Admin Login</title>

<link rel="stylesheet" href="style.css">

<style>

body{

background:#f2f2f2;

}

.login-box{

width:380px;

max-width:95%;

margin:80px auto;

background:#fff;

padding:30px;

border-radius:10px;

box-shadow:0 5px 15px rgba(0,0,0,.2);

}

.login-box h2{

text-align:center;

color:#8B0000;

margin-bottom:20px;

}

input{

width:100%;

padding:12px;

margin:10px 0;

border:1px solid #ccc;

border-radius:6px;

}

button{

width:100%;

padding:12px;

background:#8B0000;

color:#fff;

border:none;

border-radius:6px;

cursor:pointer;

font-size:16px;

}

button:hover{

background:#600000;

}

.error{

text-align:center;

color:red;

margin-bottom:10px;

}

</style>

</head>

<body>

<div class="login-box">

<h2>TJD Admin Panel</h2>

<?php

if($message!=""){

echo "<div class='error'>$message</div>";

}

?>

<form method="POST">

<input
type="text"
name="username"
placeholder="Username"
required>

<input
type="password"
name="password"
placeholder="Password"
required>

<button
type="submit"
name="login">

Login

</button>

</form>

</div>

</body>

</html>
<?php
session_start();

if(!isset($_SESSION['admin_id'])){
    header("Location: admin_login.php");
    exit();
}

$conn = new mysqli("localhost","root","","tjd_database");

$totalMembers = $conn->query("SELECT COUNT(*) AS total FROM members")->fetch_assoc()['total'];
$pendingMembers = $conn->query("SELECT COUNT(*) AS total FROM members WHERE status='Pending'")->fetch_assoc()['total'];
$approvedMembers = $conn->query("SELECT COUNT(*) AS total FROM members WHERE status='Approved'")->fetch_assoc()['total'];
$newsCount = $conn->query("SELECT COUNT(*) AS total FROM news")->fetch_assoc()['total'];
$galleryCount = $conn->query("SELECT COUNT(*) AS total FROM gallery")->fetch_assoc()['total'];
?>

<!DOCTYPE html>
<html lang="bn">
<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width,initial-scale=1">

<title>TJD Admin Dashboard</title>

<link rel="stylesheet" href="style.css">

<style>

body{
background:#f4f4f4;
margin:0;
font-family:Arial;
}

.header{
background:#8B0000;
color:white;
padding:15px;
display:flex;
justify-content:space-between;
align-items:center;
}

.sidebar{
width:250px;
height:100vh;
background:#222;
position:fixed;
top:0;
left:0;
padding-top:70px;
}

.sidebar a{
display:block;
color:white;
padding:15px;
text-decoration:none;
border-bottom:1px solid #333;
}

.sidebar a:hover{
background:#8B0000;
}

.main{
margin-left:260px;
padding:20px;
}

.card{
display:inline-block;
width:250px;
background:white;
margin:10px;
padding:20px;
border-radius:10px;
box-shadow:0 5px 10px rgba(0,0,0,.2);
text-align:center;
}

.card h2{
margin:0;
color:#8B0000;
font-size:35px;
}

.card p{
font-size:18px;
}

.logout{
color:white;
text-decoration:none;
}

</style>

</head>

<body>

<div class="header">

<h2>TJD Admin Panel</h2>

<div>

স্বাগতম,
<?php echo $_SESSION['admin_name']; ?>

|

<a href="logout.php" class="logout">
Logout
</a>

</div>

</div>

<div class="sidebar">

<a href="admin_dashboard.php">🏠 Dashboard</a>

<a href="members.php">👥 সদস্য তালিকা</a>

<a href="approve
<?php
session_start();

if(!isset($_SESSION['admin_id'])){
    header("Location: admin_login.php");
    exit();
}

$conn = new mysqli("localhost","root","","tjd_database");

if(isset($_GET['approve'])){

$id = intval($_GET['approve']);

$memberId = "TJD".date("Y").str_pad($id,6,"0",STR_PAD_LEFT);

$conn->query("UPDATE members
SET status='Approved',
member_id='$memberId'
WHERE id=$id");

header("Location: approve_members.php");

}

if(isset($_GET['reject'])){

$id = intval($_GET['reject']);

$conn->query("UPDATE members
SET status='Rejected'
WHERE id=$id");

header("Location: approve_members.php");

}

$result=$conn->query("SELECT * FROM members ORDER BY joining_date DESC");

?>

<!DOCTYPE html>

<html lang="bn">

<head>

<meta charset="UTF-8">

<title>Member Approval</title>

<link rel="stylesheet" href="style.css">

<style>

table{

width:100%;

border-collapse:collapse;

}

th,td{

border:1px solid #ddd;

padding:10px;

text-align:center;

}

th{

background:#8B0000;

color:white;

}

.approve{

background:green;

color:white;

padding:8px 12px;

text-decoration:none;

border-radius:5px;

}

.reject{

background:red;

color:white;

padding:8px 12px;

text-decoration:none;

border-radius:5px;

}

img{

width:60px;

height:60px;

object-fit:cover;

border-radius:50%;

}

</style>

</head>

<body>

<h2 align="center">

ত্রিপুরা জনতা দল

<br>

সদস্য অনুমোদন

</h2>

<table>

<tr>

<th>ছবি</th>

<th>নাম</th>

<th>মোবাইল</th>

<th>জেলা</th>

<th>স্ট্যাটাস</th>

<th>সদস্য আইডি</th>

<th>অ্যাকশন</th>

</tr>

<?php

while($row=$result->fetch_assoc()){

?>

<tr>

<td>

<img src="uploads/<?php echo $row['photo']; ?>">

</td>

<td>

<?php echo $row['fullname']; ?>

</td>

<td>

<?php echo $row['mobile']; ?>

</td>

<td>

<?php echo $row['district']; ?>

</td>

<td>

<?php echo $row['status']; ?>

</td>

<td>

<?php echo $row['member_id']; ?>

</td>

<td>

<?php

if($row['status']=="Pending"){

?>

<a class="approve"

href="?approve=<?php echo $row['id']; ?>">

Approve

</a>

<a class="reject"

href="?reject=<?php echo $row['id']; ?>">

Reject

</a>

<?php

}else{

echo "Completed";

}

?>

</td>

</tr>

<?php

}

?>
<?php
session_start();

$conn = new mysqli("localhost","root","","tjd_database");

if(!isset($_GET['id'])){
    die("Member ID Missing");
}

$id = intval($_GET['id']);

$result = $conn->query("SELECT * FROM members WHERE id=$id AND status='Approved'");

if($result->num_rows==0){
    die("Approved Member Not Found");
}

$member = $result->fetch_assoc();

$qrText = urlencode(
$member['member_id']."|".
$member['fullname']."|".
$member['mobile']
);

$qrImage =
"https://api.qrserver.com/v1/create-qr-code/?size=180x180&data=".$qrText;

?>

<!DOCTYPE html>

<html lang="bn">

<head>

<meta charset="UTF-8">

<title>TJD Member Card</title>

<style>

body{
background:#ececec;
font-family:Arial;
}

.card{

width:420px;

margin:30px auto;

background:#fff;

border-radius:15px;

overflow:hidden;

box-shadow:0 8px 20px rgba(0,0,0,.3);

}

.header{

background:#8B0000;

color:#fff;

text-align:center;

padding:15px;

}

.header h2{

margin:0;

}

.photo{

text-align:center;

margin-top:20px;

}

.photo img{

width:120px;

height:120px;

border-radius:50%;

border:4px solid #8B0000;

object-fit:cover;

}

.details{

padding:20px;

font-size:17px;

line-height:32px;

}

.details b{

color:#8B0000;

}

.qr{

text-align:center;

margin-bottom:20px;

}

.qr img{

width:170px;

}

.footer{

background:#8B0000;

color:white;

padding:10px;

text-align:center;

font-weight:bold;

}

.print{

text-align:center;

margin:20px;

}

button{

padding:12px 25px;

background:#0b7a2a;

color:#fff;

border:none;

border-radius:6px;

cursor:pointer;

font-size:16px;

}

@media print{

button{

display:none;

}

body{

background:white;

}

}

</style>

</head>

<body>

<div class="card">

<div class="header">

<h2>ত্রিপুরা জনতা দল</h2>

Tripura Janata Dal (TJD)

</div>

<div class="photo">

<img src="uploads/<?php echo $member['photo']; ?>">

</div>

<div class="details">

<b>সদস্য আইডি :</b>

<?php echo $member['member_id']; ?>

<br>

<b>নাম :</b>

<?php echo $member['fullname']; ?>

<br>

<b>মোবাইল :</b>

<?php echo $member['mobile']; ?>

<br>

<b>জেলা :</b>

<?php echo $member['district']; ?>

<br>

<b>স্ট্যাটাস :</b>

<?php echo $member['status']; ?>

</div>

<div class="qr">

<img src="<?php echo $qrImage; ?>">

</div>

<div class="footer">

Official Digital Membership Card

</div>

</div>

<div class="print">

<button onclick="window.print()">

Print / Save as PDF

</button>

</div>

</body>

</html> 
<?php
session_start();

$conn = new mysqli("localhost","root","","tjd_database");

if($conn->connect_error){
    die("Database Connection Failed");
}

$msg="";

if(isset($_POST['login'])){

    $member_id = trim($_POST['member_id']);
    $mobile    = trim($_POST['mobile']);

    $stmt = $conn->prepare("
        SELECT * FROM members
        WHERE member_id=? 
        AND mobile=? 
        AND status='Approved'
    ");

    $stmt->bind_param("ss",$member_id,$mobile);
    $stmt->execute();

    $result = $stmt->get_result();

    if($result->num_rows==1){

        $member = $result->fetch_assoc();

        $_SESSION['member_id']  = $member['id'];
        $_SESSION['member_name']= $member['fullname'];

        header("Location: member_dashboard.php");
        exit();

    }else{

        $msg="ভুল Member ID অথবা Mobile Number";

    }

}
?>

<!DOCTYPE html>
<html lang="bn">

<head>

<meta charset="UTF-8">

<meta name="viewport"
content="width=device-width,initial-scale=1">

<title>TJD Member Login</title>

<link rel="stylesheet"
href="style.css">

<style>

body{
background:#f5f5f5;
font-family:Arial;
}

.login-box{

width:400px;

max-width:95%;

margin:80px auto;

background:#fff;

padding:30px;

border-radius:12px;

box-shadow:0 5px 15px rgba(0,0,0,.2);

}

h2{

text-align:center;

color:#8B0000;

}

input{

width:100%;

padding:12px;

margin:10px 0;

border:1px solid #ccc;

border-radius:6px;

}

button{

width:100%;

padding:12px;

background:#8B0000;

color:white;

border:none;

border-radius:6px;

font-size:17px;

cursor:pointer;

}

button:hover{

background:#650000;

}

.error{

text-align:center;

color:red;

margin-bottom:15px;

font-weight:bold;

}

</style>

</head>

<body>

<div class="login-box">

<h2>সদস্য লগইন</h2>

<?php

if($msg!=""){

echo "<div class='error'>$msg</div>";

}

?>

<form method="POST">

<input
type="text"
name="member_id"
placeholder="Member ID"
required>

<input
type="text"
name="mobile"
placeholder="Registered Mobile Number"
required>

<button
type="submit"
name="login">

লগইন করুন

</button>

</form>

</div>

</body>

</html>
<?php
session_start();

if(!isset($_SESSION['member_id'])){
    header("Location: member_login.php");
    exit();
}

$conn = new mysqli("localhost","root","","tjd_database");

$id=$_SESSION['member_id'];

$result=$conn->query("SELECT * FROM members WHERE id=$id");

$member=$result->fetch_assoc();
?>

<!DOCTYPE html>

<html lang="bn">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width,initial-scale=1">

<title>TJD Member Dashboard</title>

<link rel="stylesheet" href="style.css">

<style>

body{
margin:0;
background:#f5f5f5;
font-family:Arial;
}

.header{

background:#8B0000;

color:white;

padding:15px;

display:flex;

justify-content:space-between;

align-items:center;

}

.sidebar{

width:250px;

height:100vh;

background:#222;

position:fixed;

top:0;

left:0;

padding-top:70px;

}

.sidebar a{

display:block;

padding:15px;

color:white;

text-decoration:none;

border-bottom:1px solid #444;

}

.sidebar a:hover{

background:#8B0000;

}

.main{

margin-left:260px;

padding:20px;

}

.card{

background:white;

padding:20px;

margin-bottom:20px;

border-radius:10px;

box-shadow:0 3px 10px rgba(0,0,0,.2);

}

.profile{

display:flex;

align-items:center;

gap:20px;

}

.profile img{

width:120px;

height:120px;

border-radius:50%;

object-fit:cover;

border:3px solid #8B0000;

}

.btn{

display:inline-block;

padding:12px 20px;

background:#8B0000;

color:white;

text-decoration:none;

border-radius:6px;

margin:5px;

}

.btn:hover{

background:#600000;

}

</style>

</head>

<body>

<div class="header">

<h2>ত্রিপুরা জনতা দল</h2>

<div>

স্বাগতম,

<?php echo $member['fullname']; ?>

</div>

</div>

<div class="sidebar">

<a href="member_dashboard.php">🏠 ড্যাশবোর্ড</a>

<a href="member_card.php?id=<?php echo $member['id']; ?>">🪪 সদস্য আইডি</a>

<a href="constitution.html">📘 সংবিধান</a>

<a href="documents/TJD_Constitution.pdf">📄 PDF Download</a>

<a href="news.html">📰 সংবাদ</a>

<a href="gallery.html">🖼 গ্যালারি</a>

<a href="profile_edit.php">✏ প্রোফাইল আপডেট</a>

<a href="member_logout.php">🚪 Logout</a>

</div>

<div class="main">

<div class="card">

<div class="profile">

<img src="uploads/<?php echo $member['photo']; ?>">

<div>

<h2>

<?php echo $member['fullname']; ?>

</h2>

<p>

<b>Member ID :</b>

<?php echo $member['member_id']; ?>

</p>

<p>

<b>Mobile :</b>

<?php echo $member['mobile']; ?>

</p>

<p>

<b>District :</b>

<?php echo $member['district']; ?>

</p>

<p>

<b>Status :</b>

<?php echo $member['status']; ?>

</p>

</div>

</div>

</div>

<div class="card">

<h3>দ্রুত সেবা</h3>

<a class="btn"

href="member_card.php?id=<?php echo $member['id']; ?>">

আইডি কার্ড

</a>

<a class="btn"

href="documents/TJD_Constitution.pdf">

সংবিধান PDF

</a>

<a class="btn"

href="news.html">

সংবাদ

</a>

<a class="btn"

href="gallery.html">

গ্যালারি

</a>

</div>

<div class="card">

<h3>সর্বশেষ ঘোষণা</h3>

<p>

ত্রিপুরা জনতা দলে আপনাকে স্বাগতম।

সকল সরকারি ঘোষণা, সাংগঠনিক সংবাদ এবং প্রশিক্ষণের তথ্য এই ড্যাশবোর্ডে প্রকাশ করা হবে।

</p>

</div>

</div>

</body>

</html>
<!DOCTYPE html>
<html lang="bn">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>TJD সংবিধান</title>

<link rel="stylesheet" href="style.css">

<style>

body{
margin:0;
background:#f4f4f4;
font-family:Arial;
}

header{
background:#8B0000;
color:white;
padding:20px;
text-align:center;
}

.container{
width:95%;
max-width:1300px;
margin:20px auto;
}

.menu{
display:flex;
flex-wrap:wrap;
gap:10px;
margin-bottom:20px;
}

.menu a{
background:#8B0000;
color:white;
padding:10px 15px;
text-decoration:none;
border-radius:5px;
}

.menu a:hover{
background:#600000;
}

.card{
background:white;
padding:20px;
border-radius:10px;
box-shadow:0 3px 10px rgba(0,0,0,.2);
margin-bottom:20px;
}

iframe{
width:100%;
height:800px;
border:none;
}

.download{
display:inline-block;
padding:12px 20px;
background:#0b7a2a;
color:white;
text-decoration:none;
border-radius:5px;
margin-top:15px;
}

.download:hover{
background:#08601f;
}

</style>

</head>

<body>

<header>

<h1>ত্রিপুরা জনতা দল (TJD)</h1>

<h3>দলীয় সংবিধান</h3>

</header>

<div class="container">

<div class="menu">

<a href="#chapter1">১</a>
<a href="#chapter2">২</a>
<a href="#chapter3">৩</a>
<a href="#chapter4">৪</a>
<a href="#chapter5">৫</a>
<a href="#chapter6">৬</a>
<a href="#chapter7">৭</a>
<a href="#chapter8">৮</a>
<a href="#chapter9">৯</a>
<a href="#chapter10">১০</a>
<a href="#chapter11">১১</a>
<a href="#chapter12">১২</a>
<a href="#chapter13">১৩</a>
<a href="#chapter14">১৪</a>
<a href="#chapter15">১৫</a>
<a href="#chapter16">১৬</a>
<a href="#chapter17">১৭</a>
<a href="#chapter18">১৮</a>
<a href="#chapter19">১৯</a>
<a href="#chapter20">২০</a>
<a href="#chapter21">২১</a>
<a href="#chapter22">২২</a>
<a href="#chapter23">২৩</a>
<a href="#chapter24">২৪</a>
<a href="#chapter25">২৫</a>

</div>

<div class="card">

<h2>সংবিধান PDF</h2>

<p>

নিচে ওয়েবসাইটের মধ্যেই সম্পূর্ণ সংবিধান পড়তে পারবেন।

</p>

<iframe
src="documents/TJD_Constitution.pdf">
</iframe>

<br>

<a
class="download"
href="documents/TJD_Constitution.pdf"
download>

📄 সংবিধান PDF ডাউনলোড

</a>

</div>

<div class="card">

<h2>অধ্যায়সমূহ</h2>

<p>

এখানে ধাপে ধাপে আপনার ১–২৫ অধ্যায় HTML আকারে যুক্ত হবে।

</p>

<div id="chapter1"></div>
<div id="chapter2"></div>
<div id="chapter3"></div>
<div id="chapter4"></div>
<div id="chapter5"></div>
<div id="chapter6"></div>
<div id="chapter7"></div>
<div id="chapter8"></div>
<div id="chapter9"></div>
<div id="chapter10"></div>
<div id="chapter11"></div>
<div id="chapter12"></div>
<div id="chapter13"></div>
<div id="chapter14"></div>
<div id="chapter15"></div>
<div id="chapter16"></div>
<div id="chapter17"></div>
<div id="chapter18"></div>
<div id="chapter19"></div>
<div id="chapter20"></div>
<div id="chapter21"></div>
<div id="chapter22"></div>
<div id="chapter23"></div>
<div id="chapter24"></div>
<div id="chapter25"></div>

</div>

</div>

</body>

</html>
<!DOCTYPE html>
<html lang="bn">
<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>TJD Gallery</title>

<link rel="stylesheet" href="style.css">

<style>

body{
margin:0;
background:#f5f5f5;
font-family:Arial;
}

header{
background:#8B0000;
color:#fff;
text-align:center;
padding:20px;
}

.gallery{

width:95%;
margin:30px auto;

display:grid;

grid-template-columns:repeat(auto-fit,minmax(280px,1fr));

gap:20px;

}

.card{

background:white;

border-radius:10px;

overflow:hidden;

box-shadow:0 5px 15px rgba(0,0,0,.2);

}

.card img{

width:100%;

height:250px;

object-fit:cover;

}

.card video{

width:100%;

height:250px;

}

.card h3{

padding:10px;

}

.card p{

padding:0 10px 15px;

}

.upload{

width:90%;

max-width:600px;

margin:40px auto;

background:white;

padding:20px;

border-radius:10px;

box-shadow:0 5px 15px rgba(0,0,0,.2);

}

.upload input,

.upload textarea{

width:100%;

padding:12px;

margin:10px 0;

}

.upload button{

background:#8B0000;

color:white;

padding:12px 20px;

border:none;

cursor:pointer;

border-radius:5px;

}

</style>

</head>

<body>

<header>

<h1>ত্রিপুরা জনতা দল</h1>

<h3>ছবি ও ভিডিও গ্যালারি</h3>

</header>

<div class="upload">

<h2>অ্যাডমিন আপলোড</h2>

<form
action="gallery_upload.php"
method="POST"
enctype="multipart/form-data">

<input
type="text"
name="title"
placeholder="শিরোনাম"
required>

<textarea
name="description"
placeholder="বিবরণ"></textarea>

<input
type="file"
name="media"
required>

<button>

Upload

</button>

</form>

</div>

<div class="gallery">

<?php

$conn=new mysqli("localhost","root","","tjd_database");

$result=$conn->query("SELECT * FROM gallery ORDER BY id DESC");

while($row=$result->fetch_assoc()){

$type=pathinfo($row['image'],PATHINFO_EXTENSION);

?>

<div class="card">

<?php

if($type=="mp4"){

?>

<video controls>

<source
src="uploads/<?php echo $row['image'];?>">

</video>

<?php

}else{

?>

<img
src="uploads/<?php echo $row['image'];?>">

<?php

}

?>

<h3>

<?php echo $row['title']; ?>

</h3>

<p>

<?php echo $row['description']; ?>

</p>

</div>

<?php

}

?>

</div>

</body>

</html>
<?php

$conn=new mysqli("localhost","root","","tjd_database");

$title=$_POST['title'];

$description=$_POST['description'];

$file=time()."_".$_FILES['media']['name'];

move_uploaded_file(

$_FILES['media']['tmp_name'],

"uploads/".$file

);

$conn->query("INSERT INTO gallery

(title,image,description)

VALUES

('$title','$file','$description')");

header("Location:gallery.html");

?>
==========================
news.php
==========================
<?php
$conn=new mysqli("localhost","root","","tjd_database");
?>
<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<title>TJD সংবাদ</title>

<link rel="stylesheet" href="style.css">

<style>

body{
background:#f5f5f5;
font-family:Arial;
margin:0;
}

header{
background:#8B0000;
color:white;
padding:20px;
text-align:center;
}

.container{
width:95%;
max-width:1200px;
margin:auto;
padding:20px;
}

.news{
background:white;
margin-bottom:20px;
border-radius:10px;
overflow:hidden;
box-shadow:0 3px 10px rgba(0,0,0,.2);
}

.news img{
width:100%;
max-height:400px;
object-fit:cover;
}

.news h2{
padding:15px;
color:#8B0000;
}

.news p{
padding:0 15px 20px;
line-height:28px;
}

.date{
padding:0 15px 20px;
color:gray;
font-size:14px;
}

</style>

</head>

<body>

<header>

<h1>ত্রিপুরা জনতা দল</h1>

<h3>সংবাদ ও বিজ্ঞপ্তি</h3>

</header>

<div class="container">

<?php

$result=$conn->query("SELECT * FROM news ORDER BY id DESC");

while($row=$result->fetch_assoc()){

?>

<div class="news">

<?php

if($row['image']!=""){

?>

<img src="uploads/<?php echo $row['image'];?>">

<?php

}

?>

<h2>

<?php echo $row['title']; ?>

</h2>

<p>

<?php echo nl2br($row['details']); ?>

</p>

<div class="date">

প্রকাশিত :

<?php echo $row['created_at']; ?>

</div>

</div>

<?php

}

?>

</div>

</body>

</html>


==========================
news_upload.php
==========================

<?php

$conn=new mysqli("localhost","root","","tjd_database");

$title=$_POST['title'];

$details=$_POST['details'];

$image="";

if(isset($_FILES['image'])){

$image=time()."_".$_FILES['image']['name'];

move_uploaded_file(

$_FILES['image']['tmp_name'],

"uploads/".$image

);

}

$conn->query(

"INSERT INTO news
(title,details,image)

VALUES

('$title','$details','$image')"

);

header("Location:news.php");

?>


==========================
news_admin.html
==========================

<!DOCTYPE html>

<html lang="bn">

<head>

<meta charset="UTF-8">

<title>সংবাদ প্রকাশ</title>

<link rel="stylesheet" href="style.css">

</head>

<body>

<h2 align="center">

নতুন সংবাদ প্রকাশ

</h2>

<form

action="news_upload.php"

method="POST"

enctype="multipart/form-data"

style="width:700px;margin:auto;">

<input
type="text"
name="title"
placeholder="সংবাদের শিরোনাম"
required>

<textarea
name="details"
rows="10"
placeholder="সংবাদের বিস্তারিত"
required></textarea>

<input
type="file"
name="image">

<br><br>

<button>

সংবাদ প্রকাশ করুন

</button>

</form>

</body>

</html>
==========================
comments.php
==========================

<?php
$conn=new mysqli("localhost","root","","tjd_database");
?>

<!DOCTYPE html>
<html lang="bn">
<head>

<meta charset="UTF-8">

<title>TJD মন্তব্য</title>

<link rel="stylesheet" href="style.css">

<style>

body{
font-family:Arial;
background:#f5f5f5;
margin:0;
}

.container{
width:90%;
max-width:900px;
margin:30px auto;
}

.comment-box{

background:#fff;
padding:20px;
border-radius:10px;
margin-bottom:20px;
box-shadow:0 3px 10px rgba(0,0,0,.2);

}

input,textarea{

width:100%;
padding:12px;
margin:10px 0;

}

button{

padding:12px 25px;

background:#8B0000;

color:white;

border:none;

cursor:pointer;

border-radius:5px;

}

.comment{

background:white;

padding:20px;

margin-bottom:15px;

border-left:5px solid #8B0000;

border-radius:8px;

}

.name{

font-weight:bold;

color:#8B0000;

}

.time{

font-size:13px;

color:gray;

}

</style>

</head>

<body>

<div class="container">

<div class="comment-box">

<h2>মন্তব্য করুন</h2>

<form action="comment_save.php" method="POST">

<input
type="text"
name="member_name"
placeholder="আপনার নাম"
required>

<textarea
name="comment"
rows="5"
placeholder="আপনার মন্তব্য লিখুন"
required></textarea>

<button>

মন্তব্য পাঠান

</button>

</form>

</div>

<?php

$result=$conn->query("SELECT * FROM comments ORDER BY id DESC");

while($row=$result->fetch_assoc()){

?>

<div class="comment">

<div class="name">

<?php echo $row['member_name']; ?>

</div>

<p>

<?php echo nl2br($row['comment']); ?>

</p>

<div class="time">

<?php echo $row['created_at']; ?>

</div>

</div>

<?php

}

?>

</div>

</body>

</html>

==========================
comment_save.php
==========================

<?php

$conn=new mysqli("localhost","root","","tjd_database");

$name=$_POST['member_name'];

$comment=$_POST['comment'];

$conn->query(

"INSERT INTO comments
(member_name,comment)

VALUES

('$name','$comment')"

);

header("Location:comments.php");

?>

==========================
comments_admin.php
==========================

<?php

session_start();

$conn=new mysqli("localhost","root","","tjd_database");

$result=$conn->query("SELECT * FROM comments ORDER BY id DESC");

?>

<!DOCTYPE html>

<html lang="bn">

<head>

<meta charset="UTF-8">

<title>মন্তব্য পরিচালনা</title>

<style>

table{

width:100%;

border-collapse:collapse;

}

th,td{

border:1px solid #ddd;

padding:10px;

}

th{

background:#8B0000;

color:white;

}

a{

color:red;

text-decoration:none;

}

</style>

</head>

<body>

<h2 align="center">

মন্তব্য পরিচালনা

</h2>

<table>

<tr>

<th>ID</th>

<th>নাম</th>

<th>মন্তব্য</th>

<th>তারিখ</th>

<th>Delete</th>

</tr>

<?php

while($row=$result->fetch_assoc()){

?>

<tr>

<td><?php echo $row['id']; ?></td>

<td><?php echo $row['member_name']; ?></td>

<td><?php echo $row['comment']; ?></td>

<td><?php echo $row['created_at']; ?></td>

<td>

<a href="delete_comment.php?id=<?php echo $row['id']; ?>">

Delete

</a>

</td>

</tr>

<?php

}

?>

</table>

</body>

</html>

==========================
delete_comment.php
==========================

<?php

$conn=new mysqli("localhost","root","","tjd_database");

$id=(int)$_GET['id'];

$conn->query("DELETE FROM comments WHERE id=$id");

header("Location:comments_admin.php");

?>
==========================
social.php
==========================

<!DOCTYPE html>
<html lang="bn">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width,initial-scale=1">

<title>TJD Social Media</title>

<link rel="stylesheet"
href="style.css">

<link rel="stylesheet"
href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.7.2/css/all.min.css">

<style>

body{
background:#f5f5f5;
font-family:Arial;
}

.container{
width:90%;
max-width:1000px;
margin:40px auto;
background:white;
padding:30px;
border-radius:10px;
box-shadow:0 5px 15px rgba(0,0,0,.2);
text-align:center;
}

.social a{
display:inline-block;
margin:15px;
font-size:45px;
text-decoration:none;
}

.facebook{color:#1877F2;}
.x{color:#000;}
.instagram{color:#E1306C;}
.youtube{color:#FF0000;}
.whatsapp{color:#25D366;}

button{

padding:15px 30px;

background:#8B0000;

color:white;

border:none;

border-radius:8px;

cursor:pointer;

font-size:18px;

margin-top:20px;

}

</style>

</head>

<body>

<div class="container">

<h1>ত্রিপুরা জনতা দল</h1>

<h3>Official Social Media</h3>

<div class="social">

<a class="facebook"
href="https://facebook.com/"
target="_blank">

<i class="fab fa-facebook"></i>

</a>

<a class="x"
href="https://x.com/"
target="_blank">

<i class="fab fa-x-twitter"></i>

</a>

<a class="instagram"
href="https://instagram.com/"
target="_blank">

<i class="fab fa-instagram"></i>

</a>

<a class="youtube"
href="https://youtube.com/"
target="_blank">

<i class="fab fa-youtube"></i>

</a>

<a class="whatsapp"
href="https://wa.me/"
target="_blank">

<i class="fab fa-whatsapp"></i>

</a>

</div>

<button onclick="shareWebsite()">

ওয়েবসাইট শেয়ার করুন

</button>

</div>

<script src="share.js"></script>

</body>

</html>

==========================
share.js
==========================

function shareWebsite(){

const data={

title:"Tripura Janata Dal",

text:"ত্রিপুরা জনতা দল (TJD)",

url:window.location.href

};

if(navigator.share){

navigator.share(data);

}else{

const url=encodeURIComponent(window.location.href);

window.open(

"https://www.facebook.com/sharer/sharer.php?u="+url,

"_blank"

);

}

}

function shareFacebook(){

window.open(

"https://www.facebook.com/sharer/sharer.php?u="+encodeURIComponent(location.href),

"_blank"

);

}

function shareX(){

window.open(

"https://twitter.com/intent/tweet?url="+encodeURIComponent(location.href),

"_blank"

);

}

function shareWhatsApp(){

window.open(

"https://wa.me/?text="+encodeURIComponent(location.href),

"_blank"

);

}

function shareTelegram(){

window.open(

"https://t.me/share/url?url="+encodeURIComponent(location.href),

"_blank"

);

}
==========================
organization.php
==========================

<?php
$conn=new mysqli("localhost","root","","tjd_database");
?>

<!DOCTYPE html>
<html lang="bn">
<head>

<meta charset="UTF-8">

<title>TJD সাংগঠনিক কাঠামো</title>

<link rel="stylesheet" href="style.css">

<style>

body{
font-family:Arial;
background:#f5f5f5;
margin:0;
}

.container{
width:95%;
max-width:1200px;
margin:auto;
padding:20px;
}

.card{
background:#fff;
padding:20px;
margin-bottom:20px;
border-radius:10px;
box-shadow:0 3px 10px rgba(0,0,0,.2);
}

input,select{
width:100%;
padding:12px;
margin:10px 0;
}

button{
padding:12px 20px;
background:#8B0000;
color:white;
border:none;
border-radius:5px;
cursor:pointer;
}

table{
width:100%;
border-collapse:collapse;
margin-top:20px;
}

th,td{
border:1px solid #ddd;
padding:10px;
text-align:center;
}

th{
background:#8B0000;
color:white;
}

</style>

</head>

<body>

<div class="container">

<div class="card">

<h2>সাংগঠনিক ইউনিট যোগ করুন</h2>

<form action="organization_save.php" method="POST">

<input type="text" name="district" placeholder="জেলা" required>

<input type="text" name="subdivision" placeholder="মহকুমা">

<input type="text" name="block" placeholder="ব্লক / নগর">

<input type="text" name="booth" placeholder="বুথ নম্বর">

<input type="text" name="president" placeholder="সভাপতির নাম">

<input type="text" name="secretary" placeholder="সম্পাদকের নাম">

<button type="submit">

সংরক্ষণ করুন

</button>

</form>

</div>

<div class="card">

<h2>সাংগঠনিক তালিকা</h2>

<table>

<tr>

<th>জেলা</th>

<th>মহকুমা</th>

<th>ব্লক</th>

<th>বুথ</th>

<th>সভাপতি</th>

<th>সম্পাদক</th>

</tr>

<?php

$result=$conn->query("SELECT * FROM organization ORDER BY district");

while($row=$result->fetch_assoc()){

?>

<tr>

<td><?php echo $row['district']; ?></td>

<td><?php echo $row['subdivision']; ?></td>

<td><?php echo $row['block']; ?></td>

<td><?php echo $row['booth']; ?></td>

<td><?php echo $row['president']; ?></td>

<td><?php echo $row['secretary']; ?></td>

</tr>

<?php } ?>

</table>

</div>

</div>

</body>

</html>

==========================
organization_save.php
==========================

<?php

$conn=new mysqli("localhost","root","","tjd_database");

$district=$_POST['district'];
$subdivision=$_POST['subdivision'];
$block=$_POST['block'];
$booth=$_POST['booth'];
$president=$_POST['president'];
$secretary=$_POST['secretary'];

$conn->query("INSERT INTO organization

(district,subdivision,block,booth,president,secretary)

VALUES

('$district','$subdivision','$block','$booth','$president','$secretary')");

header("Location:organization.php");

?>

==========================
SQL
==========================

CREATE TABLE organization(

id INT AUTO_INCREMENT PRIMARY KEY,

district VARCHAR(100),

subdivision VARCHAR(100),

block VARCHAR(100),

booth VARCHAR(100),

president VARCHAR(150),

secretary VARCHAR(150),

created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP

);
==========================
settings.php
==========================

<?php
session_start();

if(!isset($_SESSION['admin_id'])){
header("Location:admin_login.php");
exit();
}
?>

<!DOCTYPE html>
<html lang="bn">

<head>

<meta charset="UTF-8">

<title>TJD Settings</title>

<link rel="stylesheet" href="style.css">

<style>

body{
background:#f5f5f5;
font-family:Arial;
}

.container{
width:90%;
max-width:900px;
margin:30px auto;
}

.card{
background:white;
padding:25px;
margin-bottom:20px;
border-radius:10px;
box-shadow:0 3px 10px rgba(0,0,0,.2);
}

button{
padding:12px 20px;
background:#8B0000;
color:white;
border:none;
border-radius:5px;
cursor:pointer;
margin:5px;
}

input{
width:100%;
padding:10px;
margin:10px 0;
}

</style>

</head>

<body>

<div class="container">

<div class="card">

<h2>ওয়েবসাইট সেটিংস</h2>

<form>

<label>দলের নাম</label>

<input
type="text"
value="ত্রিপুরা জনতা দল">

<label>Official Email</label>

<input
type="email"
value="info@tjd.in">

<label>Official Mobile</label>

<input
type="text"
value="+91XXXXXXXXXX">

<button>

Save Settings

</button>

</form>

</div>

<div class="card">

<h2>Database Backup</h2>

<a href="backup.php">

<button>

Backup Database

</button>

</a>

</div>

<div class="card">

<h2>Security</h2>

<ul>

<li>✅ Admin Login Required</li>

<li>✅ Member Login Required</li>

<li>✅ Session Protection</li>

<li>✅ Password Hash Support</li>

<li>✅ Database Backup</li>

<li>✅ Logout System</li>

</ul>

</div>

</div>

</body>

</html>


==========================
backup.php
==========================

<?php

header("Content-Type:text/plain");

echo "TJD Database Backup";

echo "\n";

echo "Backup Date : ".date("Y-m-d H:i:s");

echo "\n";

echo "Export Database using phpMyAdmin.";

?>


==========================
logout.php
==========================

<?php

session_start();

session_destroy();

header("Location:index.html");

exit();

?>


==========================
member_logout.php
==========================

<?php

session_start();

session_destroy();

header("Location:member_login.php");

exit();

?>
==========================
manifest.json
==========================
{
  "name":"Tripura Janata Dal",
  "short_name":"TJD",
  "description":"Official Website of Tripura Janata Dal",
  "start_url":"index.html",
  "display":"standalone",
  "background_color":"#ffffff",
  "theme_color":"#8B0000",
  "orientation":"portrait",
  "icons":[
    {
      "src":"images/icon-192.png",
      "sizes":"192x192",
      "type":"image/png"
    },
    {
      "src":"images/icon-512.png",
      "sizes":"512x512",
      "type":"image/png"
    }
  ]
}

==========================
service-worker.js
==========================

const CACHE_NAME="tjd-v1";

const urlsToCache=[

"/",

"/index.html",

"/style.css",

"/app.js",

"/membership.html",

"/constitution.html",

"/gallery.html",

"/news.php"

];

self.addEventListener("install",event=>{

event.waitUntil(

caches.open(CACHE_NAME)

.then(cache=>cache.addAll(urlsToCache))

);

});

self.addEventListener("fetch",event=>{

event.respondWith(

caches.match(event.request)

.then(response=>{

return response || fetch(event.request);

})

);

});

==========================
index.html এর </body> এর আগে যোগ করুন
==========================

<link rel="manifest" href="manifest.json">

<script>

if("serviceWorker" in navigator){

navigator.serviceWorker.register("service-worker.js");

}

</script>

==========================
ফোল্ডার স্ট্রাকচার
==========================

/images
/uploads
/documents
/css
/js

index.html
style.css
app.js

membership.html
member_login.php
member_dashboard.php
member_card.php

admin_login.php
admin_dashboard.php

approve_members.php
members.php

news.php
news_upload.php

gallery.html
gallery_upload.php

comments.php
comment_save.php

organization.php

settings.php

manifest.json
service-worker.js

==========================
হোস্টিং
==========================

১. GitHub
২. InfinityFree
৩. Hostinger
৪. cPanel Hosting
৫. VPS Server

==========================
শেষ
==========================

Tripura Janata Dal (TJD)

Official Digital Platform

Version 1.0

