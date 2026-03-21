# Lawrenceefill
Printer Repairs and toner cartridge refill Printer sales 
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db = "lawrence_repairs";

$conn = new mysqli($host, $user, $pass, $db);

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
