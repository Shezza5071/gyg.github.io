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

body {
    background-color: black;
    color: white;
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
}

.container {
    text-align: center;
    border: 2px solid white;
    padding: 20px;
    border-radius: 10px;
    max-width: 400px;
}

.product-description {
    margin-bottom: 20px;
}

input {
    padding: 10px;
    margin: 10px 0;
    width: 100%;
    max-width: 300px;
}

#paypal-button-container {
    margin-top: 20px;
}

document.addEventListener("DOMContentLoaded", function() {
    // Your Firebase configuration
    var firebaseConfig = {
        apiKey: "YOUR_API_KEY",
        authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
        projectId: "YOUR_PROJECT_ID",
        storageBucket: "YOUR_PROJECT_ID.appspot.com",
        messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
        appId: "YOUR_APP_ID"
    };
    // Initialize Firebase
    firebase.initializeApp(firebaseConfig);
    var db = firebase.firestore();

    // Save email to Firestore
    function saveEmail(email) {
        db.collection("emails").add({
            email: email
        })
        .then(function() {
            console.log("Email saved successfully!");
        })
        .catch(function(error) {
            console.error("Error saving email: ", error);
        });
    }

    // PayPal button integration
    paypal.Buttons({
        createOrder: function(data, actions) {
            return actions.order.create({
                purchase_units: [{
                    amount: {
                        value: '10.00' // Price of the coupon
                    }
                }]
            });
        },
        onApprove: function(data, actions) {
            return actions.order.capture().then(function(details) {
                const email = document.getElementById('email').value;
                alert('Transaction completed by ' + details.payer.name.given_name);
                saveEmail(email);
            });
        }
    }).render('#paypal-button-container');
});
