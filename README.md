<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Bulk Case Margin & Price Calculator</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body { 
      font-family: Arial, sans-serif; 
      padding: 15px; 
      background-color: #f4f4f4; 
      display: flex; 
      flex-direction: column; 
      align-items: center;
      min-height: 100vh;
    }
    h2 { text-align: center; color: #333; margin-bottom: 20px; }
    .container { 
      width: 100%; 
      max-width: 450px; 
      background-color: #fff; 
      padding: 20px; 
      border-radius: 10px; 
      box-shadow: 0 2px 8px rgba(0,0,0,0.2);
    }
    label { font-weight: bold; margin-top: 10px; display: block; }
    input { 
      margin: 5px 0 15px 0; 
      padding: 12px; 
      width: 100%; 
      font-size: 16px; 
      border-radius: 5px; 
      border: 1px solid #ccc; 
      box-sizing: border-box; 
    }
    button { 
      padding: 15px; 
      width: 100%; 
      font-size: 16px; 
      border: none; 
      border-radius: 5px; 
      background-color: #4CAF50; 
      color: white; 
      cursor: pointer; 
      margin-top: 10px;
    }
    button:hover { background-color: #45a049; }
    #result { 
      margin-top: 20px; 
      font-weight: bold; 
      white-space: pre-line; 
      background-color: #f9f9f9; 
      padding: 15px; 
      border-radius: 5px; 
      border: 1px solid #ccc; 
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Bulk Case Margin & Price Calculator</h2>

    <label>Cost of Case ($):</label>
    <input type="number" id="costCase" step="0.01" placeholder="Enter total cost of the case">

    <label>Number of Units in Case:</label>
    <input type="number" id="unitsCase" step="1" placeholder="Enter number of units in the case">

    <label>Target Margin (%) (optional):</label>
    <input type="number" id="marginCase" step="0.01" placeholder="Enter target margin %">

    <label>Selling Price per Unit ($) (optional):</label>
    <input type="number" id="priceUnit" step="0.01" placeholder="Enter selling price per unit">

    <button onclick="calculate()">Calculate</button>

    <p id="result"></p>
  </div>

  <script>
    function calculate() {
      let costCase = parseFloat(document.getElementById("costCase").value);
      let unitsCase = parseFloat(document.getElementById("unitsCase").value);
      let margin = parseFloat(document.getElementById("marginCase").value);
      let priceUnit = parseFloat(document.getElementById("priceUnit").value);

      if (isNaN(costCase) || costCase <= 0 || isNaN(unitsCase) || unitsCase <= 0) {
        document.getElementById("result").innerText = "⚠️ Please enter valid cost and number of units.";
        return;
      }

      let costPerUnit = costCase / unitsCase;
      let resultText = `Cost per Unit: $${costPerUnit.toFixed(2)}\n`;

      if (!isNaN(margin) && margin > 0 && margin < 100) {
        let calculatedPrice = costPerUnit / (1 - margin / 100);
        resultText += `Target Margin: ${margin.toFixed(2)}%\nSelling Price per Unit (calculated): $${calculatedPrice.toFixed(2)}\n`;
      }

      if (!isNaN(priceUnit) && priceUnit > 0) {
        let actualMargin = ((priceUnit - costPerUnit) / priceUnit) * 100;
        resultText += `Entered Selling Price per Unit: $${priceUnit.toFixed(2)}\nGross Margin Achieved: ${actualMargin.toFixed(2)}%`;
      }

      if ((isNaN(margin) || margin <= 0 || margin >= 100) && (isNaN(priceUnit) || priceUnit <= 0)) {
        resultText += "⚠️ Please enter either a target margin or selling price per unit.";
      }

      document.getElementById("result").innerText = resultText;
    }
  </script>
</body>
</html>
