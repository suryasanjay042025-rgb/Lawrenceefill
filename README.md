# Lawrenceefill
Printer Repairs and toner cartridge refill Printer sales 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Lawrence Computer & Printer Repairs</title>

<style>
body {
    margin: 0;
    font-family: 'Segoe UI', sans-serif;
    background: #f5f7fa;
}

header {
    background: #111827;
    color: white;
    display: flex;
    justify-content: space-between;
    padding: 20px;
}

nav a {
    color: white;
    margin-left: 20px;
    text-decoration: none;
}

.hero {
    text-align: center;
    padding: 100px 20px;
    background: linear-gradient(135deg,#007bff,#00c6ff);
    color: white;
}

.btn {
    padding: 12px 25px;
    background: black;
    color: white;
    border-radius: 8px;
    text-decoration: none;
}

.section {
    padding: 40px;
    text-align: center;
}

.cards {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px;
}

.card {
    background: white;
    padding: 25px;
    border-radius: 12px;
    width: 250px;
    box-shadow: 0 10px 25px rgba(0,0,0,0.1);
}

.product {
    border: 1px solid #ccc;
    padding: 20px;
    margin: 15px;
    border-radius: 10px;
}

.whatsapp {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background: green;
    color: white;
    padding: 15px;
    border-radius: 50px;
    text-decoration: none;
}

footer {
    background: #111;
    color: white;
    text-align: center;
    padding: 20px;
}
</style>
</head>

<body>

<header>
    <h2>Lawrence Repairs</h2>
    <nav>
        <a href="#home">Home</a>
        <a href="#services">Services</a>
        <a href="#shop">Shop</a>
        <a href="#contact">Contact</a>
    </nav>
</header>

<!-- HERO -->
<section class="hero" id="home">
    <h1>Computer & Printer Repairs</h1>
    <p>Fast • Affordable • Reliable in Bengaluru</p>
    <a href="#shop" class="btn">Shop Now</a>
</section>

<!-- SERVICES -->
<section class="section" id="services">
    <h2>Our Services</h2>
    <div class="cards">
        <div class="card">
            <h3>💻 Laptop Repair</h3>
            <p>Screen, battery, motherboard fixes</p>
        </div>

        <div class="card">
            <h3>🖨 Printer Repair</h3>
            <p>Ink, cartridge, paper jam solutions</p>
        </div>

        <div class="card">
            <h3>⚡ Upgrades</h3>
            <p>SSD, RAM, speed optimization</p>
        </div>
    </div>
</section>

<!-- SHOP -->
<section class="section" id="shop">
    <h2>Shop</h2>

    <div class="product">
        <h3>SSD 512GB</h3>
        <p>₹4500</p>
        <a href="https://wa.me/919448477226?text=I want SSD">Buy via WhatsApp</a>
    </div>

    <div class="product">
        <h3>Printer Cartridge</h3>
        <p>₹1200</p>
        <a href="https://wa.me/919448477226?text=I want cartridge">Buy via WhatsApp</a>
    </div>

    <br>

    <!-- Razorpay Payment Button -->
    <button id="pay-btn">Pay ₹500</button>

</section>

<!-- QR -->
<section class="section">
    <h2>Scan QR</h2>
    <p>Add your QR image here (qr.png)</p>
</section>

<!-- CONTACT -->
<section class="section" id="contact">
    <h2>Contact</h2>
    <p><strong>Anthony Lawrence</strong></p>
    <p>📍 Byrathi, Bengaluru 560077</p>
    <p>📞 +91 94484 77226</p>
    <p>📧 anthony.lawrence1987@gmail.com</p>
</section>

<footer>
    <p>© 2026 Lawrence Repairs</p>
</footer>

<!-- WhatsApp Button -->
<a href="https://wa.me/919448477226" class="whatsapp">💬 Chat</a>

<!-- Razorpay Script -->
<script src="https://checkout.razorpay.com/v1/checkout.js"></script>
<script>
var options = {
    "key": "YOUR_RAZORPAY_KEY",
    "amount": "50000",
    "currency": "INR",
    "name": "Lawrence Repairs",
    "description": "Service Payment",
    "handler": function (response){
        alert("Payment Successful!");
    }
};

document.getElementById('pay-btn').onclick = function(e){
    var rzp = new Razorpay(options);
    rzp.open();
    e.preventDefault();
}
</script>

</body>
</html>
