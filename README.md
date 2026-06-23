<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Password Strength Detector</title>

<style>
    body {
        font-family: Arial, sans-serif;
        background: linear-gradient(135deg, #667eea, #764ba2);
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
    }

    .container {
        background: white;
        padding: 30px;
        border-radius: 15px;
        box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        width: 350px;
        text-align: center;
    }

    h2 {
        margin-bottom: 20px;
    }

    input {
        width: 100%;
        padding: 12px;
        border: 2px solid #ddd;
        border-radius: 8px;
        font-size: 16px;
        box-sizing: border-box;
    }

    .strength-bar {
        width: 100%;
        height: 10px;
        background: #ddd;
        border-radius: 10px;
        margin-top: 15px;
        overflow: hidden;
    }

    .bar {
        height: 100%;
        width: 0%;
        transition: 0.3s;
    }

    #strength-text {
        margin-top: 10px;
        font-weight: bold;
    }
</style>
</head>
<body>

<div class="container">
    <h2>Password Strength Detector</h2>

    <input type="password" id="password" placeholder="Enter Password">

    <div class="strength-bar">
        <div class="bar" id="bar"></div>
    </div>

    <p id="strength-text">Strength: None</p>
</div>

<script>
const password = document.getElementById("password");
const bar = document.getElementById("bar");
const strengthText = document.getElementById("strength-text");

password.addEventListener("input", () => {
    let pass = password.value;
    let score = 0;

    if (pass.length >= 8) score++;
    if (/[A-Z]/.test(pass)) score++;
    if (/[a-z]/.test(pass)) score++;
    if (/[0-9]/.test(pass)) score++;
    if (/[^A-Za-z0-9]/.test(pass)) score++;

    switch(score) {
        case 0:
        case 1:
            bar.style.width = "20%";
            bar.style.background = "red";
            strengthText.textContent = "Strength: Very Weak";
            break;

        case 2:
            bar.style.width = "40%";
            bar.style.background = "orange";
            strengthText.textContent = "Strength: Weak";
            break;

        case 3:
            bar.style.width = "60%";
            bar.style.background = "gold";
            strengthText.textContent = "Strength: Medium";
            break;

        case 4:
            bar.style.width = "80%";
            bar.style.background = "lightgreen";
            strengthText.textContent = "Strength: Strong";
            break;

        case 5:
            bar.style.width = "100%";
            bar.style.background = "green";
            strengthText.textContent = "Strength: Very Strong";
            break;
    }

    if(pass.length === 0){
        bar.style.width = "0%";
        strengthText.textContent = "Strength: None";
    }
});
</script>

</body>
</html>
