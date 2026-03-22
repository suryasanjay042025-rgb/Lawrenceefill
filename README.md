
CREATE DATABASE lawrence_enterprise;
USE lawrence_enterprise;

CREATE TABLE admins (
 id INT AUTO_INCREMENT PRIMARY KEY,
 username VARCHAR(100),
 password VARCHAR(255)
);

INSERT INTO admins (username,password)
VALUES ('admin','admin123');

CREATE TABLE products (
 id INT AUTO_INCREMENT PRIMARY KEY,
 name VARCHAR(200),
 price DECIMAL(10,2),
 stock INT
);

CREATE TABLE cart (
 id INT AUTO_INCREMENT PRIMARY KEY,
 product_id INT,
 qty INT
);

CREATE TABLE orders (
 id INT AUTO_INCREMENT PRIMARY KEY,
 total DECIMAL(10,2),
 status VARCHAR(50) DEFAULT 'Pending'
);

CREATE TABLE repairs (
 id INT AUTO_INCREMENT PRIMARY KEY,
 tracking_id VARCHAR(50),
 customer_name VARCHAR(150),
 phone VARCHAR(50),
 device VARCHAR(150),
 issue TEXT,
 status VARCHAR(100) DEFAULT 'Received'
);
<?php
session_start();

$conn = new mysqli("localhost","root","","lawrence_enterprise");
if($conn->connect_error){ die("DB Error"); }

/* ========= LOGIN ========= */
if(isset($_POST['login'])){
    if($_POST['u']=="admin" && $_POST['p']=="admin123"){
        $_SESSION['admin']=true;
    }
}

/* ========= CART ========= */
if(!isset($_SESSION['cart'])) $_SESSION['cart']=[];
if(isset($_GET['add'])){
    $id=$_GET['add'];
    $_SESSION['cart'][$id]=($_SESSION['cart'][$id]??0)+1;
}

/* ========= REPAIR ========= */
function trackID(){
 return "LCR-".date("Y")."-".rand(10000,99999);
}

if(isset($_POST['repair'])){
 $tid=trackID();
 $n=$_POST['name']; $p=$_POST['phone']; $d=$_POST['device']; $i=$_POST['issue'];
 $conn->query("INSERT INTO repairs(tracking_id,customer_name,phone,device,issue) VALUES('$tid','$n','$p','$d','$i')");
 echo "<h3>Your Tracking ID: $tid</h3>";
}

/* ========= PAGE ========= */
$page=$_GET['page']??'home';
?>

<!DOCTYPE html>
<html>
<head>
<title>Lawrence Enterprise</title>
<style>
body{font-family:Segoe UI;margin:0;background:#f5f7fa;}
header{background:#111;color:#fff;padding:15px;text-align:center;}
nav a{color:#fff;margin:10px;}
.section{text-align:center;padding:40px;}
.card{background:#fff;padding:20px;margin:10px;border-radius:10px;}
.btn{padding:10px;background:#007bff;color:#fff;}
</style>
</head>

<body>

<header>
<h2>Lawrence Enterprise System</h2>
<nav>
<a href="?">Home</a>
<a href="?page=shop">Shop</a>
<a href="?page=cart">Cart</a>
<a href="?page=repair">Repair</a>
<a href="?page=admin">Admin</a>
</nav>
</header>

<?php if($page=="home"): ?>
<div class="section"><h1>Enterprise System Ready 🚀</h1></div>

<?php elseif($page=="shop"): ?>

<div class="section">
<h2>Products</h2>

<?php
$res=$conn->query("SELECT * FROM products");
while($p=$res->fetch_assoc()){
echo "<div class='card'>";
echo $p['name']." ₹".$p['price'];
echo "<br><a href='?add=".$p['id']."' class='btn'>Add</a>";
echo "</div>";
}
?>
</div>

<?php elseif($page=="cart"): ?>

<div class="section">
<h2>Cart</h2>

<?php
$total=0;
foreach($_SESSION['cart'] as $id=>$qty){
$r=$conn->query("SELECT * FROM products WHERE id=$id")->fetch_assoc();
$subtotal=$r['price']*$qty;
$total+=$subtotal;
echo "<div class='card'>".$r['name']." x $qty = ₹$subtotal</div>";
}
echo "<h3>Total: ₹$total</h3>";
$_SESSION['total']=$total;
?>

<a href="?page=checkout" class="btn">Checkout</a>
</div>

<?php elseif($page=="checkout"): ?>

<div class="section">
<h2>Payment</h2>

<button id="pay-btn">Pay ₹<?=$_SESSION['total']?></button>

<script src="https://checkout.razorpay.com/v1/checkout.js"></script>
<script>
var options = {
 "key":"YOUR_RAZORPAY_KEY",
 "amount":"<?=$_SESSION['total']*100?>",
 "currency":"INR",
 "name":"Lawrence Repairs",
 "handler":function(){
  alert("Payment Successful");
 }
};
document.getElementById('pay-btn').onclick=function(e){
 new Razorpay(options).open(); e.preventDefault();
}
</script>

</div>

<?php elseif($page=="repair"): ?>

<div class="section">
<h2>Book Repair</h2>
<form method="POST">
<input name="name" placeholder="Name"><br>
<input name="phone"><br>
<input name="device"><br>
<textarea name="issue"></textarea><br>
<button name="repair">Submit</button>
</form>
</div>

<?php elseif($page=="admin"): ?>

<div class="section">

<?php if(!isset($_SESSION['admin'])): ?>

<form method="POST">
<input name="u"><input name="p" type="password">
<button name="login">Login</button>
</form>

<?php else: ?>

<h2>Admin Panel</h2>

<h3>Add Product</h3>
<form method="POST">
<input name="name"><input name="price">
<button name="addp">Add</button>
</form>

<?php
if(isset($_POST['addp'])){
$n=$_POST['name'];$pr=$_POST['price'];
$conn->query("INSERT INTO products(name,price,stock) VALUES('$n','$pr',10)");
}
?>

<?php endif; ?>

</div>

<?php endif; ?>

</body>
</html>
