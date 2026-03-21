efill-printer-service/
│
├── backend/
│   ├── server.js
│   ├── models/ServiceRequest.js
│   ├── routes/serviceRoutes.js
│   └── .env
│
└── frontend/
    ├── pages/
    │   ├── index.js
    │   └── contact.js
    ├── components/
    │   └── Navbar.js
    └── styles/globals.css
    <!DOCTYPE html>
<html>
<head>
  <title>Contact</title>
  <link rel="stylesheet" href="style.css">
</head>

<body>

<nav>
  <h2>Contact</h2>
</nav>

<div class="container">

  <h1>Contact Us</h1>

  <form>
    <input placeholder="Name"><br><br>
    <input placeholder="Email"><br><br>
    <textarea placeholder="Message"></textarea><br><br>

    <button class="btn btn-primary">Send</button>
  </form>

</div>

</body>
</html>
