# Day 39 – PDF Splitter & Merger

## Interactive Productivity Applications

### Project: Foliate – PDF Splitter & Merger

For Day 39 of the #60DayClaudeChallenge, I built **Foliate**, a browser-based PDF utility that allows users to split PDF documents into specific ranges and merge multiple PDF files into a single document.

The application focuses on privacy, simplicity and a polished productivity-focused user experience.

---

## 🚀 Features

### 📄 PDF Splitter

The splitter supports multiple ways of processing a PDF:

- Custom page ranges
- Split after specific pages
- Split every N pages
- Extract selected pages
- Page-by-page PDF preview
- Page selection
- Result file preview
- Individual PDF downloads
- Download all split files as a ZIP

### 📎 PDF Merger

The merger allows users to:

- Upload multiple PDF files
- Preview uploaded files
- Arrange files in the required order
- Display total file count
- Display total page count
- Set a custom output filename
- Merge PDFs into a single document
- Download the generated PDF

### 🔐 Privacy-Focused Processing

The application is designed to process PDF data directly in the browser.

Key characteristics:

- Client-side PDF processing
- No PDF upload to a backend server
- Works offline after required libraries are loaded
- Files remain within the browser workflow

### 🎨 User Interface

The application includes:

- Premium dark interface
- Light/dark theme toggle
- Drag-and-drop upload
- Responsive layout
- PDF page thumbnails
- Progress indicators
- Toast notifications
- Interactive buttons and controls
- Keyboard-friendly interactions

---

## 🛠️ Technologies Used

- HTML5
- CSS3
- JavaScript
- PDF.js
- pdf-lib
- LocalStorage
- Browser File API

PDF.js is used for rendering PDF page previews, while pdf-lib is used for PDF document processing.

---

# 📸 Screenshots

## 1. PDF Splitter Dashboard

![PDF Splitter Dashboard](images/01-splitter-dashboard.png)

The splitter provides a drag-and-drop interface for uploading a PDF and selecting different splitting methods.

---

## 2. PDF Splitter Results

![PDF Splitter Results](images/02-splitter-result.png)

After processing, the application displays the generated PDF files with their page counts and provides download options.

In my test, the application generated five output PDF files from the uploaded document:

- Week-1_A_part1.pdf – 3 pages
- Week-1_A_part2.pdf – 4 pages
- Week-1_A_part3.pdf – 3 pages
- Week-1_A_part4.pdf – 3 pages
- Week-1_A_part5.pdf – 10 pages

---

## 3. PDF Merger Dashboard

![PDF Merger Dashboard](images/03-merger-dashboard.png)

The merger allows multiple PDF files to be uploaded and arranged before creating the final document.

---

## 4. PDF Merge Result

![PDF Merge Result](images/04-merge-result.png)

The merger successfully processed four PDF files and generated a single merged document.

Test result:

- Files merged: 4
- Total pages: 198
- Output: merged.pdf

---

# 🧠 What I Learned

### 1. Client-Side File Processing

I learned how browser-based applications can process files directly without requiring a traditional backend server.

### 2. Working with PDF Libraries

I learned how PDF.js can be used to render PDF pages for preview and how pdf-lib can be used for PDF manipulation.

### 3. Building Interactive Workflows

The project helped me understand how to design a complete workflow:

Upload → Preview → Configure → Process → Download

### 4. Drag-and-Drop Interfaces

I learned how drag-and-drop interactions can make document management applications easier to use.

### 5. PDF Page Management

I explored different ways of selecting and organising pages, including page ranges, page extraction and splitting based on page counts.

### 6. Multiple File Processing

The merger helped me understand how multiple uploaded files can be handled, ordered and combined into one output document.

### 7. Progress and User Feedback

I learned how progress indicators and toast notifications can improve the user experience during file processing.

### 8. Privacy-Focused Applications

This project showed me how useful productivity tools can be designed around client-side processing so that sensitive documents do not need to be uploaded to a server.

---

# 💡 Key Takeaway

My biggest takeaway from this project was understanding how a relatively simple browser application can become a useful productivity tool when the workflow is carefully designed.

The combination of:

**Upload → Preview → Select → Process → Download**

creates a complete document-processing experience without requiring a traditional backend.

---

# 🤖 AI-Assisted Development

Claude was used as an AI development assistant during the creation of this project.

I used the generated HTML application locally, tested the splitter and merger workflows, processed PDF files and verified the generated outputs.

---

# 📅 Challenge

Day 39 of the #60DayClaudeChallenge.

#60DayClaudeChallenge
