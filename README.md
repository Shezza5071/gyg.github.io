<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Guzman y Gomez Coupon</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Guzman y Gomez Coupon</h1>
        <div class="product-description">
            <p>Get your Guzman y Gomez coupon worth $10. Enjoy delicious meals with this special offer!</p>
        </div>
        <form id="purchaseForm">
            <label for="email">Enter your email:</label>
            <input type="email" id="email" name="email" required>
            <div id="paypal-button-container"></div>
        </form>
    </div>
    <script src="https://www.paypal.com/sdk/js?client-id=YOUR_PAYPAL_CLIENT_ID"></script>
    <script src="https://www.gstatic.com/firebasejs/8.6.8/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.6.8/firebase-firestore.js"></script>
    <script src="script.js"></script>
</body>
</html>
