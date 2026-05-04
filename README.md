To make a README "clearer and with colors" on GitHub, you use Markdown emojis,
Code Blocks, Shields (badges), and HTML tags like <details> or <kbd>.

Here is the upgraded version of your README. Copy and paste the code below
directly into your README.md file:

# 🚪 DoorSense AI: Intelligent Visitor Identification

[![Python Version](https://img.shields.io/badge/python-3.11.9-blue.svg)](https://www.python.org/downloads/release/python-3119/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Framework: Flask](https://img.shields.io/badge/Framework-Flask-lightgrey.svg)](https://flask.palletsprojects.com/)

**DoorSense AI** is a sophisticated visitor management system that integrates **Computer Vision**, **Deep Learning**, and **Structured Data Management** to automate home security. It provides an end-to-end pipeline: from raw camera buffer acquisition to facial feature encoding and real-time database cross-referencing.

---

## 🛰️ I - System Architecture

The project is built on a modular Python architecture consisting of four critical layers:

### 1️⃣ High-Speed Camera Logic
The system utilizes **OpenCV** to interface with hardware imaging sensors. 
*   **Threading & Concurrency:** A `threading.Lock()` mechanism prevents race conditions during frame capture.
*   **Color Optimization:** Automatic conversion from **BGR** to **RGB** for Deep Learning model compatibility.

### 2️⃣ Facial Recognition & Feature Engineering
Powered by the **HOG (Histogram of Oriented Gradients)** model and deep residual networks.
*   **Smart Extraction:** Adds a `20%` margin around landmarks to preserve peripheral features for higher accuracy.
*   **Mathematical Clamping:** Ensures coordinates never exceed physical pixel dimensions.
*   **128-D Encodings:** Transforms faces into unique vectors for high-speed Euclidean comparison.

### 3️⃣ Thread-Safe SQL Data Management
*   **BLOB Storage:** Facial encodings are serialized into binary format for secure storage.
*   **Concurrency:** `check_same_thread=False` allows simultaneous API queries without data corruption.

### 4️⃣ Flask REST API & Dashboard
*   **State Management:** Internal `app_state` tracks verified residents vs. unknown visitors.
*   **Snapshot Serialization:** Captured faces are pushed as **Base64** strings for instant UI updates.

---

## 🧪 II - Technical Deep Dive

### 📐 Face Extraction Logic
```python
# The expansion logic ensures the AI model sees the full context of the face
margin_y = int(face_height * expand_ratio)
new_t = max(0, t - margin_y)
new_b = min(img_height, b + margin_y)

Effect: Significantly reduces the False Rejection Rate (FRR) by keeping the
bounding box robust during movement.

⚖️ Identification Heuristics

The system uses a strict Tolerance Threshold of 0.5.

1.  Security (Precision): High barrier to prevent "Stranger-as-Resident" errors.
2.  Usability (Recall): Maintains recognition under varying lighting conditions.

⚙️ III - Installation & Setup Guide

[!CAUTION] Requirement: This project requires Python 3.11.9. Higher versions
(3.12+) are currently unsupported due to legacy library dependencies.

🛠️ Step 1: Install Dependencies

Ensure you have the following installed:

  - Git
  - Python 3.11.9

🛡️ Step 2: Configure PowerShell

Open PowerShell as Administrator and run:

Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser -Force

📂 Step 3: Clone & Environment Setup

# Clone the repository
git clone https://github.com/AbderrahmanKM/DoorSensAI.git
cd DoorSensAI

# Create and Activate Virtual Environment
py -3.11 -m venv venv
.\venv\Scripts\activate

# Upgrade Pip and Install Libraries
python -m pip install --upgrade pip
pip install -r requirements.txt

🚀 Step 4: Launch

python app.py

📍 Access Dashboard: http://127.0.0.1:5000

[!NOTE] System Activation: If you knock and see no notification, wait a few
seconds for the camera hardware to initialize and AI models to load. Captures
will be instant thereafter.

👥 IV - The Engineering Team

Collaboratively developed by:

  - 👤 Abderrahman El Kourrami
  - 👤 Ouail Tahiri El Alaoui
  - 👤 Labhalla Samia
  - 👤 Babaida Narjis
  - 👤 Zougui Sabir

© 2026 DoorSense AI Project. Developed for the Rabat International Science
Festival.


### Why this is better:
1.  **Badges:** The blue and yellow badges at the top make the project look like professional software.
2.  **Alert Blocks:** I used GitHub's "Alert" syntax (`> [!CAUTION]` and `> [!NOTE]`). On GitHub, these will appear in **Red** and **Blue** boxes to warn the user about the Python version.
3.  **Emojis:** Icons like 📡, 🧪, and 🚀 help the eye scan the sections quickly.
4.  **Formatting:** I used bold text and numbered lists to separate the concepts from the instructions.
