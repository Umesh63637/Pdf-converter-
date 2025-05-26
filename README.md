const express = require("express");
const cors = require("cors");
const multer = require("multer");

const app = express();
const port = 4000;

app.use(cors());
app.use(express.json());

const upload = multer({ storage: multer.memoryStorage() });

// Simple text summary function
function summarize(text) {
  return text.length > 100 ? text.slice(0, 100) + "..." : text;
}

// Serve frontend HTML
app.get("/", (req, res) => {
  res.send(`
  <!DOCTYPE html>
  <html>
  <head><title>Simple Text Summarizer & Upload</title></head>
  <body>
    <h1>Simple Text Summarizer & File Upload</h1>

    <h3>Summarize Text</h3>
    <textarea id="inputText" rows="6" cols="50"></textarea><br/>
    <button onclick="summarizeText()">Summarize</button>
    <p><b>Summary:</b> <span id="summary"></span></p>

    <h3>Upload File</h3>
    <input type="file" id="fileInput" />
    <button onclick="uploadFile()">Upload</button>
    <p id="uploadStatus"></p>

    <script>
      async function summarizeText() {
        const text = document.getElementById('inputText').value;
        if (!text.trim()) {
          alert('Please enter text to summarize.');
          return;
        }
        const response = await fetch('/api/summarize', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ text })
        });
        const data = await response.json();
        document.getElementById('summary').textContent = data.summary;
      }

      async function uploadFile() {
        const input = document.getElementById('fileInput');
        if (input.files.length === 0) {
          alert('Please select a file to upload.');
          return;
        }
        const formData = new FormData();
        formData.append('file', input.files[0]);
        const response = await fetch('/upload', {
          method: 'POST',
          body: formData
        });
        const data = await response.json();
        document.getElementById('uploadStatus').textContent = data.message + ' (' + data.filename + ')';
      }
    </script>
  </body>
  </html>
  `);
});

// Summarize API
app.post("/api/summarize", (req, res) => {
  const { text } = req.body;
  if (!text) return res.status(400).json({ error: "No text provided" });
  const summary = summarize(text);
  res.json({ summary });
});

// Upload API
app.post("/upload", upload.single('file'), (req, res) => {
  if (!req.file) return res.status(400).json({ error: "No file uploaded" });
  res.json({ message: "File uploaded successfully", filename: req.file.originalname });
});

app.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});
