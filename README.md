# PetAgeMatch
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0"> <title>Same Age as Your Dog</title> <style>
    body {
        font-family: 'Quicksand', sans-serif;
        background: #f0f9f9;
        margin: 0;
        padding: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        min-height: 100vh;
        color: #333;
    }

    header {
        text-align: center;
        padding: 40px 20px 20px 20px;
    }

    header h1 {
        font-size: 2.5em;
        margin-bottom: 10px;
        color: #2c7a7b;
    }

    header p {
        font-size: 1.2em;
        color: #555;
    }

    main {
        background: #ffffff;
        padding: 30px;
        border-radius: 15px;
        box-shadow: 0 5px 20px rgba(0,0,0,0.1);
        width: 90%;
        max-width: 500px;
        text-align: center;
    }

    label {
        display: block;
        margin: 15px 0 5px 0;
        font-weight: 600;
    }

    input, select {
        padding: 10px;
        width: 80%;
        font-size: 1em;
        border-radius: 8px;
        border: 1px solid #ccc;
    }

    button {
        margin-top: 20px;
        padding: 12px 25px;
        font-size: 1.1em;
        border: none;
        border-radius: 10px;
        background-color: #2c7a7b;
        color: white;
        cursor: pointer;
        transition: 0.3s;
    }

    button:hover {
        background-color: #285e61;
    }

    #result {
        margin-top: 25px;
        font-size: 1.2em;
        font-weight: 600;
        color: #d53f8c;
    }

    .illustration {
        margin-top: 25px;
    }

    .timeline {
        margin-top: 30px;
        text-align: left;
        font-size: 0.9em;
    }

    .paw {
        display: inline-block;
        margin: 0 3px;
        color: #d53f8c;
        font-size: 1.2em;
    }

    @media(max-width: 500px){
        input, select {
            width: 100%;
        }
    }
</style>
</head>
<body>

<header>
    <h1>🐶 Same Age as Your Dog?</h1>
    <p>Find the exact date you and your dog will be the same age!</p> </header>

<main>
    <label for="yourDob">Your Birthdate:</label>
    <input type="date" id="yourDob">

    <label for="dogDob">Dog's Birthdate:</label>
    <input type="date" id="dogDob">

    <label for="dogSize">Dog Size (optional):</label>
    <select id="dogSize">
        <option value="medium">Medium</option>
        <option value="small">Small</option>
        <option value="large">Large</option>
    </select>

    <button onclick="calculateCrossover()">Calculate Crossover Date</button>

    <p id="result"></p>

    <div class="illustration">
        🧑‍🦱➡️🐾🐶
    </div>

    <div class="timeline">
        <strong>Timeline (Human vs Dog Age in Human Years):</strong><br>
        Human: 0 <span class="paw">🐾</span> 10 <span class="paw">🐾</span> 20 <span class="paw">🐾</span> 30 <span class="paw">🐾</span> 40<br>
        Dog: 0 <span class="paw">🐾</span> 2 <span class="paw">🐾</span> 4 <span class="paw">🐾</span> 6 <span class="paw">🐾</span> 8 <span class="paw">🐾</span> 10
    </div>
</main>

<script>
function calculateCrossover() {
    const yourDob = new Date(document.getElementById('yourDob').value);
    const dogDob = new Date(document.getElementById('dogDob').value);
    const dogSize = document.getElementById('dogSize').value;

    if(!yourDob || !dogDob){
        alert("Please select both birthdates!");
        return;
    }

    const msInYear = 1000 * 60 * 60 * 24 * 365.25;

    // Human age now
    const yourAge = (Date.now() - yourDob.getTime()) / msInYear;

    // Dog age now
    const dogAge = (Date.now() - dogDob.getTime()) / msInYear;

    // Adjust dog-human conversion based on size (more accurate)
    let multiplier = 7; // default medium
    if(dogSize === "small") multiplier = 6.5;
    else if(dogSize === "large") multiplier = 7.5;

    // Calculate dog age in human years
    let targetDogAge = yourAge / multiplier;

    // Target date when crossover happens
    let targetDate = new Date(dogDob.getTime() + targetDogAge * msInYear);

    document.getElementById('result').innerText =
        "🎉 You and your dog will be the same age on: " + targetDate.toDateString(); } </script>

</body>
</html>
