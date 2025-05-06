<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Voltage Drop Calculator (Copper Wire)</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 2em; }
    label, input, select { margin: 0.5em 0; display: block; }
    .result { margin-top: 1em; font-weight: bold; }
  </style>
</head>
<body>
  <h1>Voltage Drop Calculator (Copper Only)</h1>

  <label for="length">Length of Wire (one-way) in feet:</label>
  <input type="number" id="length" placeholder="e.g. 100" required>

  <label for="current">Current (Amps):</label>
  <input type="number" id="current" placeholder="e.g. 10" required>

  <label for="awg">Wire Gauge (AWG):</label>
  <select id="awg">
    <option value="6530">12 AWG</option>
    <option value="4110">14 AWG</option>
  </select>

  <label for="voltage">Source Voltage (e.g., 12V or 24V):</label>
  <input type="number" id="voltage" placeholder="e.g. 12" required>

  <button onclick="calculateDrop()">Calculate</button>

  <div class="result" id="output"></div>

  <script>
    function calculateDrop() {
      const K = 12.9; // copper constant
      const L = parseFloat(document.getElementById('length').value);
      const I = parseFloat(document.getElementById('current').value);
      const CM = parseFloat(document.getElementById('awg').value);
      const V_source = parseFloat(document.getElementById('voltage').value);

      if (isNaN(L) || isNaN(I) || isNaN(CM) || isNaN(V_source)) {
        document.getElementById('output').innerText = "Please fill in all fields correctly.";
        return;
      }

      const V_drop = (2 * K * L * I) / CM;
      const percentDrop = (V_drop / V_source) * 100;

      document.getElementById('output').innerText =
        `Voltage Drop: ${V_drop.toFixed(2)} V\nVoltage Drop Percentage: ${percentDrop.toFixed(2)}%`;
    }
  </script>
</body>
</html>

