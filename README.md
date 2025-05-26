<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>PDF Multi-Tool Converter</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f7f9fc;
      margin: 0;
      padding: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
    }
    h1 {
      color: #333;
      margin-bottom: 10px;
    }
    .container {
      background: #fff;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      padding: 30px;
      max-width: 500px;
      width: 100%;
      text-align: center;
    }
    input[type="file"] {
      margin: 15px 0;
    }
    button {
      background: #007bff;
      border: none;
      padding: 12px 20px;
      border-radius: 5px;
      color: white;
      font-weight: bold;
      cursor: pointer;
      transition: background 0.3s ease;
    }
    button:hover {
      background: #0056b3;
    }
    .result {
      margin-top: 20px;
      font-size: 16px;
      color: #444;
    }
  </style>
</head>
<body>
  <h1>PDF Multi-Tool Converter</h1>
  <div class="container">
    <input type="file" id="pdfFile" accept="application/pdf" />
    <div>
      <button onclick="convertPDF('toText')">Convert to Text</button>
      <button onclick="convertPDF('toImages')">Convert to Images</button>
      <button onclick="convertPDF('compress')">Compress PDF</button>
    </div>
    <div class="result" id="result"></div>
  </div>

  <script>
    function convertPDF(action) {
      const fileInput = document.getElementById('pdfFile');
      const result = document.getElementById('result');
      if (!fileInput.files.length) {
        result.textContent = 'Please upload a PDF file first.';
        return;
      }
      const file = fileInput.files[0];
      result.textContent = `Processing "${file.name}" for action: ${action}...`;

      // Simulated processing (replace with real PDF library code)
      setTimeout(() => {
        switch(action) {
          case 'toText':
            result.textContent = `Converted "${file.name}" to text successfully! (demo)`;
            break;
          case 'toImages':
            result.textContent = `Converted "${file.name}" pages to images successfully! (demo)`;
            break;
          case 'compress':
            result.textContent = `Compressed "${file.name}" successfully! (demo)`;
            break;
          default:
            result.textContent = 'Unknown action.';
        }
      }, 1500);
    }
  </script>
</body>
</html>
