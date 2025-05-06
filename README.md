<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Voltage Drop Calculator </title>
  <style>
    body { font-family: Arial, sans-serif; margin: 2em; max-width: 600px; }
    label, input, select { margin: 0.5em 0; display: block; width: 100%; }
    button { margin-top: 1em; padding: 0.5em 1em; font-size: 1em; }
    .result { margin-top: 1.5em; font-weight: bold; font-size: 1.1em; }
    .disclaimer { margin-top: 2em; font-size: 0.9em; color: #555; border-top: 1px solid #ccc; padding-top: 1em; }
  </style>
</head>
<body>
  <h1>Voltage Drop Calculator </h1>

  <label for="length">Length of Wire (Feet) :</label>
  <input type="number" id="length" placeholder="e.g. 100" required>

  <label for="current">Current (Amps):</label>
  <input type="number" id="current" placeholder="e.g. 10" required>

  <label for="awg">Wire Gauge (AWG):</label>
  <select id="awg">
    <option value="6530">12 AWG</option>
    <option value="4110">14 AWG</option>
  </select>

  <label for="voltage">Source Voltage:</label>
  <select id="voltage">
    <option value="12">12 V</option>
    <option value="13">13 V</option>
    <option value="14">14 V</option>
    <option value="15">15 V</option>
  </select>

  <button onclick="calculateDrop()">Calculate</button>

  <div class="result" id="output"></div>

  <div class="disclaimer">
    ⚠️ <strong>Note:</strong> For optimal performance and to ensure safe operation of low-voltage lighting systems, the voltage at the fixture should not drop below <strong>10.5 volts</strong>. Excessive voltage drop can result in dim or malfunctioning fixtures and potential long-term damage.
  </div>

  <script>
    function calculateDrop() {
      const K = 12.9; // copper constant
      const L = parseFloat(document.getElementById('length').value);
      const I = parseFloat(document.getElementById('current').value);
      const CM = parseFloat(document.getElementById('awg').value);
      const V_source = parseFloat(document.getElementById('voltage').value);

      if (isNaN(L) || isNaN(I) || isNaN(CM) || isNaN(V_source)) {
        document.getElementById('output').innerText = "⚠️ Please fill in all fields correctly.";
        return;
      }

      const V_drop = (2 * K * L * I) / CM;
      const V_end = V_source - V_drop;

      document.getElementById('output').innerText =
        `🔋 Voltage Drop: ${V_drop.toFixed(2)} V\\n⚡ Voltage at Fixture: ${V_end.toFixed(2)} V`;
    }
  </script>
</body>
</html>


