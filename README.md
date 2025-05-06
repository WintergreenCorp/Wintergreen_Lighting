<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Voltage Drop Calculator </title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 600px; margin: auto; padding: 20px; }
        label { display: block; margin-top: 10px; }
        input, select { width: 100%; padding: 8px; margin-top: 5px; }
        button { margin-top: 15px; padding: 10px 20px; }
        .result { margin-top: 20px; font-weight: bold; font-size: 1.1em; }
        .status-good { color: green; font-weight: bold; }
        .status-bad { color: red; font-weight: bold; }
        .disclaimer { margin-top: 20px; font-size: 0.9em; color: #555; }
    </style>
</head>
<body>
    <h2>Voltage Drop Calculator </h2>
    <label for="voltage">Source Voltage:</label>
    <select id="voltage">
        <option value="12">12V</option>
        <option value="13">13V</option>
        <option value="14">14V</option>
        <option value="15">15V</option>
    </select>

    <label for="distance">One-Way Distance (ft):</label>
    <input type="number" id="distance" placeholder="Enter distance in feet">

    <label for="wattage">Load Wattage (W):</label>
    <input type="number" id="wattage" placeholder="Enter wattage">

    <label for="gauge">Wire Gauge:</label>
    <select id="gauge">
        <option value="12">12 AWG</option>
        <option value="14">14 AWG</option>
    </select>

    <button onclick="calculateDrop()">Calculate Voltage</button>
    <div class="result" id="result"></div>
    <div class="disclaimer">
        ⚠️ In professional lighting systems, voltage at the load should not drop below 10.5V. Ensure wire sizing and power requirements maintain safe operational levels.
    </div>

    <script>
        const resistancePer1000Ft = {
            "12": 1.588,
            "14": 2.525
        };

        function calculateDrop() {
            const voltage = parseFloat(document.getElementById("voltage").value);
            const distance = parseFloat(document.getElementById("distance").value);
            const wattage = parseFloat(document.getElementById("wattage").value);
            const gauge = document.getElementById("gauge").value;

            const resultDiv = document.getElementById("result");

            if (isNaN(distance) || isNaN(wattage)) {
                resultDiv.innerHTML = "Please enter valid distance and wattage.";
                return;
            }

            const resistance = resistancePer1000Ft[gauge] / 1000; // Ohms per foot
            const current = wattage / voltage;
            const voltageDrop = 2 * distance * resistance * current;
            const finalVoltage = voltage - voltageDrop;

            const status = finalVoltage >= 10.5
                ? "<span class='status-good'>✔️ Good</span>"
                : "<span class='status-bad'>❌ Overloaded</span>";

            resultDiv.innerHTML = `
                Voltage at load: ${finalVoltage.toFixed(2)}V<br>
                Voltage drop: ${voltageDrop.toFixed(2)}V<br>
                ${status}
            `;
        }
    </script>
</body>
</html>

