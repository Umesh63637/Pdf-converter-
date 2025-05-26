<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>PDFProX — The Smartest Way to Handle Your PDFs</title>
  <style>
    * {
      box-sizing: border-box;
    }
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      margin: 0;
      background: #f4f7fa;
      color: #333;
      text-align: center;
    }
    header {
      background: linear-gradient(135deg, #005eff, #00c8ff);
      color: white;
      padding: 2rem 1rem;
      animation: fadeIn 1s ease;
    }
    h1.headline {
      font-size: 3rem;
      margin: 0;
    }
    p.subline {
      font-size: 1.2rem;
      margin-top: 0.5rem;
    }
    .tools {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 2rem;
      padding: 3rem 1rem;
      max-width: 1100px;
      margin: 0 auto;
    }
    .tool {
      background: white;
      border-radius: 16px;
      padding: 1.5rem;
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.07);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      cursor: pointer;
      user-select: none;
    }
    .tool:hover,
    .tool:focus {
      transform: translateY(-10px);
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
      outline: none;
    }
    .tool img {
      width: 80px;
      margin-bottom: 1rem;
      pointer-events: none;
    }
    .tool h2 {
      margin: 0.5rem 0 0.3rem;
    }
    .tool p {
      color: #555;
      font-size: 0.95rem;
      margin: 0;
    }
    footer {
      background: #222;
      color: #aaa;
      padding: 1.5rem 1rem;
      font-size: 0.9rem;
      user-select: none;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(-20px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .tool:focus-visible {
      outline: 3px solid #00c8ff;
      outline-offset: 4px;
    }
  </style>
</head>
<body>
  <header>
    <h1 class="headline" tabindex="0">PDFProX</h1>
    <p class="subline">Fast. Free. No Sign Up. Your PDF Superpowers.</p>
  </header>

  <main class="tools" role="main">
    <div class="tool" tabindex="0" role="button" aria-label="Open PDF to Word converter"
      onclick="toolAction('PDF to Word', 'pdf-to-word.html')">
      <img src="https://img.icons8.com/ios-filled/100/0000FF/pdf-2.png" alt="PDF to Word Icon" />
      <h2>PDF to Word</h2>
      <p>Convert PDF into editable Word docs instantly.</p>
    </div>

    <div class="tool" tabindex="0" role="button" aria-label="Open Word to PDF converter"
      onclick="toolAction('Word to PDF', 'word-to-pdf.html')">
      <img src="https://img.icons8.com/ios-filled/100/0000FF/ms-word.png" alt="Word to PDF Icon" />
      <h2>Word to PDF</h2>
      <p>Turn Word documents into secure PDFs.</p>
    </div>

    <div class="tool" tabindex="0" role="button" aria-label="Open Merge PDFs tool"
      onclick="toolAction('Merge PDFs', 'merge-pdf.html')">
      <img src="https://img.icons8.com/ios-filled/100/0000FF/pdf-doc.png" alt="Merge PDFs Icon" />
      <h2>Merge PDFs</h2>
      <p>Combine multiple PDFs into one smooth file.</p>
    </div>

    <div class="tool" tabindex="0" role="button" aria-label="Open Compress PDF tool"
      onclick="toolAction('Compress PDF', 'compress-pdf.html')">
      <img src="https://img.icons8.com/ios-filled/100/0000FF/compress.png" alt="Compress PDF Icon" />
      <h2>Compress PDF</h2>
      <p>Shrink PDF size without losing quality.</p>
    </div>

    <div class="tool" tabindex="0" role="button" aria-label="Open Image to PDF converter"
      onclick="toolAction('Image to PDF', 'image-to-pdf.html')">
      <img src="https://img.icons8.com/ios-filled/100/0000FF/image.png" alt="Image to PDF Icon" />
      <h2>Image to PDF</h2>
      <p>Convert images (JPG, PNG) into PDF files easily.</p>
    </div>
  </main>

  <footer>
    <p>Secure &amp; Private — Files are never stored.</p>
    <p>© 2025 PDFProX. Built for speed &amp; simplicity.</p>
  </footer>

  <script>
    function toolAction(toolName, link) {
      const notif = document.createElement('div');
      notif.textContent = `${toolName} Tool Loading...`;
      notif.style.position = 'fixed';
      notif.style.top = '20px';
      notif.style.left = '50%';
      notif.style.transform = 'translateX(-50%)';
      notif.style.background = '#005eff';
      notif.style.color = 'white';
      notif.style.padding = '1rem 2rem';
      notif.style.borderRadius = '8px';
      notif.style.boxShadow = '0 4px 12px rgba(0,0,0,0.3)';
      notif.style.opacity = '0';
      notif.style.fontWeight = '600';
      notif.style.zIndex = '9999';
      notif.style.transition = 'opacity 0.4s ease';

      document.body.appendChild(notif);
      requestAnimationFrame(() => {
        notif.style.opacity = '1';
      });

      setTimeout(() => {
        notif.style.opacity = '0';
        notif.addEventListener('transitionend', () => {
          notif.remove();
          if (link) window.location.href = link;
        });
      }, 2000);
    }
  </script>
</body>
</html>
