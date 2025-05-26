<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>PDFProX - Fast Free PDF Tools</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #f4f7fa;
      color: #333;
      text-align: center;
    }
    header {
      background: linear-gradient(135deg, #005eff, #00c8ff);
      color: white;
      padding: 3rem 1rem 2rem;
    }
    header h1 {
      font-size: 3rem;
      margin-bottom: 0.5rem;
    }
    header p {
      font-size: 1.2rem;
    }
    .tools {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 2rem;
      padding: 3rem 1rem;
      max-width: 1100px;
      margin: auto;
    }
    .tool {
      background: white;
      border-radius: 12px;
      padding: 1.5rem;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
      transition: 0.3s ease;
      cursor: pointer;
    }
    .tool:hover {
      transform: translateY(-6px);
    }
    .tool img {
      width: 60px;
      margin-bottom: 1rem;
    }
    .tool h2 {
      font-size: 1.2rem;
      color: #005eff;
    }
    .tool p {
      font-size: 0.9rem;
      color: #666;
    }
    footer {
      background: #222;
      color: #aaa;
      padding: 1.5rem 1rem;
      font-size: 0.9rem;
    }
    .notification {
      position: fixed;
      top: 20px;
      left: 50%;
      transform: translateX(-50%);
      background: #005eff;
      color: white;
      padding: 0.8rem 1.2rem;
      border-radius: 8px;
      font-weight: bold;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
      z-index: 1000;
      display: none;
    }
  </style>
</head>
<body>

<header>
  <h1>PDFProX</h1>
  <p>Fast. Free. No Sign Up. Your PDF Superpowers.</p>
</header>

<main class="tools">
  <div class="tool" onclick="openTool('PDF to Word', 'tool/pdf-to-word.html')">
    <img src="https://img.icons8.com/ios-filled/100/005eff/pdf-2.png" alt="PDF to Word Icon">
    <h2>PDF to Word</h2>
    <p>Convert PDFs into editable Word files</p>
  </div>

  <div class="tool" onclick="openTool('Word to PDF', 'tool/word-to-pdf.html')">
    <img src="https://img.icons8.com/ios-filled/100/005eff/ms-word.png" alt="Word to PDF Icon">
    <h2>Word to PDF</h2>
    <p>Turn Word documents into PDFs</p>
  </div>

  <div class="tool" onclick="openTool('Merge PDFs', 'tool/merge-pdf.html')">
    <img src="https://img.icons8.com/ios-filled/100/005eff/pdf.png" alt="Merge PDFs Icon">
    <h2>Merge PDFs</h2>
    <p>Combine multiple PDFs into one</p>
  </div>

  <div class="tool" onclick="openTool('Compress PDF', 'tool/compress-pdf.html')">
    <img src="https://img.icons8.com/ios-filled/100/005eff/compress.png" alt="Compress PDF Icon">
    <h2>Compress PDF</h2>
    <p>Reduce PDF file size easily</p>
  </div>

  <div class="tool" onclick="openTool('Image to PDF', 'tool/image-to-pdf.html')">
    <img src="https://img.icons8.com/ios-filled/100/005eff/image.png" alt="Image to PDF Icon">
    <h2>Image to PDF</h2>
    <p>Convert JPG/PNG images to PDF</p>
  </div>
</main>

<footer>
  <p>Secure &amp; Private — Files are never stored.</p>
  <p>&copy; 2025 PDFProX. Built for speed &amp; simplicity.</p>
</footer>

<div class="notification" id="notif">Loading...</div>

<script>
  function openTool(toolName, url) {
    const notif = document.getElementById("notif");
    notif.textContent = toolName + " Loading...";
    notif.style.display = "block";

    setTimeout(() => {
      window.location.href = url;
    }, 1500);
  }
</script>

</body>
</html>
