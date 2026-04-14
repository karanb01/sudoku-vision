# 🧩 Sudoku Vision Solver

> Point a camera at any Sudoku puzzle. Watch it solve itself.

A Computer Vision + AI pipeline that detects a Sudoku grid from a live camera or image,
recognizes the digits, solves the puzzle using backtracking, and overlays the solution
back onto the original frame in real time.

Built as a learning project — DSA, Computer Vision, and Python, all in one.

---

## 🧠 How It Works

```
Camera / Image
      ↓
Grid Detection       (OpenCV — find and isolate the 9×9 grid)
      ↓
Digit Recognition    (OCR / pre-trained model — read each cell)
      ↓
Solver               (Backtracking algorithm — pure Python logic)
      ↓
Overlay              (Draw solution back onto the original frame)
```

---

## 🏗️ Build Phases

### Phase 1 — The Solver (Pure Logic)
**Goal:** Build a working Sudoku solver in Python with zero dependencies on camera or image input.

- Input: a 9×9 Python array with `0` representing empty cells
- Output: the fully solved 9×9 grid
- Algorithm: **Recursive Backtracking** with constraint checking
- No OpenCV, no camera — just clean logic

This phase is intentionally isolated. The solver is the brain of the entire project.
Get this right, and the rest is plumbing.

**Key concepts practiced:** Recursion, backtracking, constraint propagation, 2D arrays

---

### Phase 2 — The Reader (Static Image Input)
**Goal:** Take a photo of a real Sudoku puzzle and extract the grid + digits from it.

- Detect and isolate the Sudoku grid from the image using contour detection
- Correct perspective (handle tilted / angled photos)
- Split the grid into 81 individual cells
- Recognize the digit in each cell using OCR or a pre-trained digit classifier
- Feed the extracted grid into the Phase 1 solver

**Key concepts practiced:** OpenCV contour detection, perspective transform, image preprocessing, digit recognition (pytesseract or TensorFlow Lite)

> ⚠️ This is the hardest phase. Lighting, angles, handwritten vs printed digits
> all add complexity. Take it one sub-problem at a time.

---

### Phase 3 — Live Camera + Real-Time Overlay
**Goal:** Make it work live — point a webcam at a puzzle and see the solution drawn on screen.

- Open webcam feed using OpenCV `VideoCapture`
- Run the Phase 2 pipeline on each frame (or every N frames for performance)
- Once puzzle is detected and solved, overlay the missing digits on the live frame
- Display in a real-time window

**Key concepts practiced:** Real-time video processing, frame rate optimization, overlay rendering, pipeline integration

---

## 🛠️ Tech Stack

| Layer | Tool |
|---|---|
| Language | Python 3.10+ |
| Image processing | OpenCV |
| Digit recognition | pytesseract / TensorFlow Lite |
| Solver | Pure Python (backtracking) |
| Environment | venv / conda |
| IDE | VS Code |

---

## 📁 Project Structure

```
sudoku-vision/
├── solver/
│   └── solver.py            # Phase 1 — backtracking solver
├── vision/
│   ├── grid_extractor.py    # Phase 2 — grid detection + perspective fix
│   └── digit_recognizer.py  # Phase 2 — OCR / digit classification
├── main.py                  # Phase 3 — live camera pipeline
├── test_images/             # Sample Sudoku images for testing
├── requirements.txt
└── README.md
```

---

## 🚀 Future Scope

This project has a natural growth path. Once the core pipeline is solid, here's where it can go:

### 📱 Mobile App
- Port the solver and vision pipeline to a mobile app (Android/iOS)
- Use the phone camera directly — no webcam needed
- Frameworks to explore: **Kivy** (Python), **Flutter + Python backend**, or **React Native + OpenCV.js**
- Could be a standalone offline app — no internet required to solve

### 🤖 Better Digit Recognition
- Train a custom CNN (Convolutional Neural Network) on printed + handwritten Sudoku digits
- Makes the reader far more robust across different puzzle styles and fonts

### 🌐 Web App Version
- Flask or FastAPI backend — upload an image, get the solved puzzle back
- Simple frontend with a file upload and solution overlay display
- Could be deployed on a cloud platform (AWS / GCP / Render)

### ⚡ Performance Optimization
- Optimize the real-time pipeline for lower-end hardware
- Skip frames intelligently, cache detected grids, reduce redundant computation

### 🧩 Puzzle Generator
- Generate valid Sudoku puzzles of varying difficulty
- Add a difficulty rating system based on solving technique complexity

### 📊 Solver Analytics
- Show *how* the puzzle was solved — which cells were filled in which order
- Visualize the backtracking process as an animation (great for DSA learning)

### 🗃️ Puzzle Archive
- Scan, solve, and save puzzles from newspapers or books into a local database
- Search and replay solved puzzles later

---

## 📌 Status

- [x] Repo initialized
- [ ] Phase 1 — Solver (in progress)
- [ ] Phase 2 — Static image reader
- [ ] Phase 3 — Live camera + overlay

---

*Learning project. Built to understand, not just to ship.*