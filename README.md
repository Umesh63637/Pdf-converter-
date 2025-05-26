import express from "express";
import cors from "cors";
import multer from "multer";

const app = express();
const port = 4000;

app.use(cors());
app.use(express.json());

const upload = multer({ storage: multer.memoryStorage() });

// Simple AI summary function: truncate to 100 chars
function summarize(text) {
  return text.length > 100 ? text.slice(0, 100) + "..." : text;
}

// Serve simple frontend HTML
app.get("/", (req, res) => {
  res.send(`
    <!DOCTYPE html>
    <html lang="en">
    <head><meta charset="UTF-8" /><title>AI PDF Converter</title></head>
    <body>
      <h1>AI PDF Converter Simple Demo</h1>
      
      <h3>Text Summarizer</h3>
      <textarea id="inputText" rows="6" cols="50" placeholder="Paste text to summarize"></textarea><br/>
      <button onclick="summarizeText()">Summarize</button>
      <p><b>Summary:</b> <span id="summary"></span></p>

      <h3>File Upload</h3>
      <input type="file" id="fileInput" multiple />
      <button onclick="uploadFiles()">Upload Files</button>
      <ul id="fileList"></ul>

      <script>
        async function summarizeText() {
          const text = document.getElementById('inputText').value;
          if (!text.trim()) {
            alert('Enter text to summarize');
            return;
          }
          document.getElementById('summary').textContent = 'Loading...';
          try {
            const res = await fetch('/api/ai/summarize', {
              method: 'POST',
              headers: { 'Content-Type': 'application/json' },
              body: JSON.stringify({ text })
            });
            const data = await res.json();
            document.getElementById('summary').textContent = data.summary || 'No summary returned';
          } catch {
            document.getElementById('summary').textContent = 'Error calling API';
          }
        }

        async function uploadFiles() {
          const input = document.getElementById('fileInput');
          const files = input.files;
          if (files.length === 0) {
            alert('Select files to upload');
            return;
          }
          const list = document.getElementById('fileList');
          list.innerHTML = '';
          for (let i = 0; i < files.length; i++) {
            const file = files[i];
            const formData = new FormData();
            formData.append('file', file);
            try {
              const res = await fetch('/upload', {
                method: 'POST',
                body: formData
              });
              const data = await res.json();
              const li = document.createElement('li');
              li.textContent = data.message + ' (' + data.filename + ')';
              list.appendChild(li);
            } catch {
              const li = document.createElement('li');
              li.textContent = 'Upload failed: ' + file.name;
              list.appendChild(li);
            }
          }
        }
      </script>
    </body>
    </html>
  `);
});

// API endpoint to summarize text
app.post("/api/ai/summarize", (req, res) => {
  const { text } = req.body;
  if (!text) return res.status(400).json({ error: "Missing text input" });

  const summary = summarize(text);
  res.json({ summary });
});

// API endpoint to upload a single file
app.post("/upload", upload.single("file"), (req, res) => {
  if (!req.file) return res.status(400).json({ error: "No file uploaded" });
  res.json({ message: "File received", filename: req.file.originalname });
});

app.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});
