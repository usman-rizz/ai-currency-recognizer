<div align="center">

# *💵 AICurrency~Recognizor*

### <em>See the note. Understand the image. Recognize the denomination.</em>

<p>
  A local computer-vision application that recognizes Pakistani banknote denominations
  from camera captures or uploaded images.
</p>

<p>
  <img src="https://img.shields.io/badge/Node.js-18%2B-339933?style=for-the-badge&logo=node.js&logoColor=white" alt="Node.js 18 or newer">
  <img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python 3.10 or newer">
  <img src="https://img.shields.io/badge/OpenCV-Computer%20Vision-5C3EE8?style=for-the-badge" alt="OpenCV">
  <img src="https://img.shields.io/badge/scikit--learn-ML-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" alt="scikit-learn">
  <img src="https://img.shields.io/badge/SQLite-Local%20Storage-003B57?style=for-the-badge&logo=sqlite&logoColor=white" alt="SQLite">
</p>

<p>
  <strong>Local Windows App</strong> &nbsp;•&nbsp;
  <strong>Responsive Web UI</strong> &nbsp;•&nbsp;
  <strong>HOG + Colour Features + RBF SVM</strong>
</p>

</div>

---

## ⚡ At a glance

**AICurrency~Recognizor** is more than a single ML script. It connects a browser-based interface, Node.js backend, Python computer-vision pipeline, trained classifier, and local scan history into one working application.

| | |
|---|---|
| **Purpose** | Pakistani Rupee denomination recognition |
| **Supported classes** | PKR 10, 20, 50, 100, 500, 1000, 5000 |
| **Input** | Camera capture, front/back upload |
| **Model** | RBF SVM with HOG + colour features |
| **Storage** | SQLite + local image storage |
| **Mode** | Local Windows application |

> ⚠️ **Important:** The system predicts a likely denomination. It does **not** determine whether a banknote is genuine, fake, or counterfeit.

---

## ✨ Key features

- 📷 **Camera + upload workflow** — capture or upload front/back images directly from the browser.
- 🔎 **Recognition + confidence** — returns a denomination with confidence-aware reporting.
- 🖼️ **Image-quality checks** — blur, brightness, contrast, resolution, readability, and possible edge damage.
- 🔄 **Easy retake controls** — rotate, remove, retake, or turn the camera off when needed.
- 📊 **Scan history** — successful/unsuccessful attempts, confidence, denomination, sides used, and statistics.
- 👤 **Local accounts** — sign-up, login, sign-out, demo Google sign-in, and plan presentation.
- 💾 **Local saving** — optionally keep scan images on the computer.
- 🧠 **Project transparency** — model, dataset, and low-data status are visible inside the application.

---

## 🏗️ System Architecture

> **Architecture diagram goes here**

<p align="center">
  <img src="Architecture/img.png" alt="AICurrency~Recognizor system architecture" width="900">
</p>

### Request flow

```text
Camera / Upload
      ↓
Browser UI
      ↓
Node.js + Express
      ↓
Python JSON Bridge
      ↓
Quality Checks + Feature Extraction
      ↓
RBF SVM Prediction
      ↓
SQLite History + Result
      ↓
Recognition / Confidence / Guidance
```

The Node.js layer handles the web interface, HTTP requests, and upload validation. The Python layer performs image-quality checks, prediction, history operations, and local image persistence through a JSON bridge. The trained model is stored with `joblib`, while scan records are stored in SQLite.

---

## 🤖 Machine-learning pipeline

| Stage | Approach |
|---|---|
| Dataset discovery | Finds supported images inside denomination folders |
| Validation | Pillow + OpenCV check readability and minimum image size |
| Duplicate control | SHA-256 fingerprints prevent duplicate counting |
| Preprocessing | Shared preprocessing for training and inference |
| Features | HOG for shapes/edges + colour histograms |
| Augmentation | Controlled image variations for training diversity |
| Classifier | `StandardScaler` + RBF-kernel `SVC` with probability estimates |
| Confidence | Configurable threshold reduces weak forced predictions |
| Artifacts | `joblib` model + JSON metadata |

### Current dataset

The current dataset contains **25 valid unique images across 7 denomination classes**.

| Denomination | Front | Back | Total |
|---|---:|---:|---:|
| PKR 10 | 5 | 5 | 10 |
| PKR 20 | 1 | 1 | 2 |
| PKR 50 | 1 | 1 | 2 |
| PKR 100 | 1 | 1 | 2 |
| PKR 500 | 1 | 1 | 2 |
| PKR 1000 | 3 | 2 | 5 |
| PKR 5000 | 1 | 1 | 2 |
| **Total** | **13** | **12** | **25** |

> 📌 The model is operational, but the project is still in **low-data mode**. More varied training images are needed for stronger real-world reliability.

**Dataset targets:** minimum 12 images per denomination • recommended 30 • ideal balance around 15 front + 15 back per class.

---

## 📁 Dataset structure

```text
dataset/
└── images/
    ├── PKR_10/
    │   ├── front/
    │   └── back/
    ├── PKR_20/
    │   ├── front/
    │   └── back/
    ├── PKR_50/
    │   ├── front/
    │   └── back/
    ├── PKR_100/
    │   ├── front/
    │   └── back/
    ├── PKR_500/
    │   ├── front/
    │   └── back/
    ├── PKR_1000/
    │   ├── front/
    │   └── back/
    └── PKR_5000/
        ├── front/
        └── back/
```

### Good training images

Keep the complete note inside the frame, use even lighting, avoid glare/shadows, keep important text visible, and capture both sides. Avoid screenshots, downloaded images, and duplicate copies as training data.

---

## 🧰 Technology stack

**Frontend:** HTML5, CSS3, Vanilla JavaScript, browser MediaDevices API

**Backend:** Node.js 18+, Express 4.x, Multer 2.x, JSON/multipart HTTP APIs

**ML / Computer Vision:** Python 3.10+, OpenCV, Pillow, NumPy, scikit-image, scikit-learn, joblib

**Storage / Testing:** SQLite, pytest, SHA-256 fingerprinting, Windows batch scripts

---

## 📡 API

| Endpoint | Method | Purpose |
|---|---|---|
| `/api/health` | `GET` | Checks that the Node.js service is running |
| `/api/predict` | `POST` | Receives front/back images and runs recognition |
| `/api/scans` | `POST` | Saves optional images and scan data |
| `/api/history` | `GET` | Returns scan history and statistics |
| `/api/model` | `GET` | Returns model and dataset metadata |

Health response:

```json
{"ok":true}
```

---

## 🚀 Run locally on Windows

### Requirements

- Python 3.10+
- Node.js 18+
- Chrome, Edge, or another modern browser

### Start the application

1. Open the project folder.
2. Add images to the correct denomination/front/back folders.
3. Run **`START_PROJECT.bat`**.
4. The script prepares the Python environment, validates the dataset, trains/reuses the model, installs Node dependencies, and starts the Express server.
5. Open:

```text
http://localhost:3000
```

Keep the command window open while using the application. Press `Ctrl + C` to stop the server.

### Retrain the model

After adding new training images:

```text
TRAIN_MODEL.bat
```

Then start the app again with:

```text
START_PROJECT.bat
```

### Test the server

Open:

```text
http://localhost:3000/api/health
```

Expected:

```json
{"ok":true}
```

## 🐳 Run with Docker

Docker runs the Node.js server and Python model pipeline in one reproducible container. The existing Windows setup remains unchanged; use Docker only when Docker Desktop is installed and running.

### Requirements

- Docker Desktop for Windows
- Hardware virtualization enabled in BIOS/UEFI if Docker Desktop requests it

### Start the container

From the project folder, either double-click:

```text
DOCKER_RUN.bat
```

or run:

```powershell
docker compose up --build
```

The first build installs Node.js and Python dependencies, validates the dataset, and trains the model inside the image. Open `http://localhost:3000` after the container starts.

The local `data` folder is mounted into the container so scan history and saved images remain available after the container is recreated.

### Useful Docker commands

```powershell
# Start in the background
docker compose up --build -d

# View application logs
docker compose logs -f

# Check the running container
docker compose ps

# Stop the application
docker compose down

# Rebuild after adding dataset images
docker compose down
docker compose build --no-cache
docker compose up
```

To create an explicitly tagged image:

```powershell
docker build -t aicurrency-recognizor:local .
```

The Docker image contains the trained model generated during the build. After changing images in `dataset/images`, rebuild the image so the new dataset is used.


## ⚠️ Limitations

- The current dataset is small and unbalanced.
- Confidence is not proof of note authenticity.
- Blur, glare, shadows, cropping, and unusual backgrounds can reduce confidence.
- Note-condition analysis is visual guidance only.
- Local history and saved scans remain on the computer.
- Demo authentication and checkout flows are not production services.
- Real-world reliability requires a larger, more varied evaluation dataset.

---

## 🔐 Privacy & production notes

This is a **local academic/project prototype**. Local account information, scan history, and saved images remain on the computer. The Google sign-in and checkout interfaces are demonstrations; they are not real OAuth or payment processing.

Before public deployment, the system would need secure server-side authentication/authorization, password hashing, HTTPS, protected storage, backups, logging, rate limiting, a PCI-compliant payment provider, and a separately labelled authenticity model.

---

## 🛣️ Next improvements

| Priority | Improvement |
|---:|---|
| 1 | Increase the dataset to at least 12 and preferably 30 images per denomination |
| 2 | Create a separate untouched evaluation set for honest accuracy measurement |
| 3 | Compare the current SVM pipeline with a compact transfer-learning model |
| 4 | Build a dedicated authenticity dataset with expert-labelled genuine/counterfeit examples |
| 5 | Move authentication, permissions, history, and payments to secure server-side services |

---

<div align="left">

## **👨‍💻 About the Author**

### Muhammad Usman

> *Data Enthusiast | Machine Learning Learner | Clean Coding Practitioner*

---

## **🔗 Connect With Me**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/mohammad-usman736/)  [![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:usman.rizz6769@gmail.com)  [![Hotmail](https://img.shields.io/badge/Outlook-0078D4?style=for-the-badge&logo=microsoft-outlook&logoColor=white)](mailto:Muhammad_usman2023@hotmail.com)

</div>
