# DoorSense AI: Real-Time Intelligent Visitor Identification

DoorSense AI is a sophisticated visitor management system that integrates
Computer Vision, Deep Learning, and structured data management to automate home
security. The system provides an end-to-end pipeline: from raw camera buffer
acquisition to facial feature encoding and real-time database cross-referencing.

I- System Architecture

The project is built on a modular Python architecture consisting of four
critical layers:

1. High-Speed Camera Logic

The system utilizes OpenCV to interface with hardware imaging sensors. To ensure
the UI remains responsive while the AI processes frames, the camera logic is
decoupled from the main execution thread.

  - Threading & Concurrency: A threading.Lock() mechanism is implemented to
    prevent race conditions during frame capture.
  - Color Space Conversion: Frames are captured in BGR and converted to RGB for
    compatibility with Deep Learning models.

2. Facial Recognition & Feature Engineering

At the heart of the system is the HOG (Histogram of Oriented Gradients) model
combined with a deep residual network.

  - Extraction Logic: The system doesn't just crop faces; it uses a custom
    expand_ratio algorithm to add a 20% margin around detected landmarks. This
    ensures that the peripheral features needed for high-accuracy encoding are
    preserved.
  - Boundary Clamping: To prevent runtime errors, the code implements
    mathematical clamping (min/max) to ensure extracted coordinates never exceed
    the physical pixel dimensions of the raw frame.
  - 128-D Encodings: Each face is transformed into a 128-dimensional vector
    (linear embedding), allowing for high-speed Euclidean distance comparison.

3. Thread-Safe SQL Data Management

The system utilizes an SQLite backend to store registered profiles.

  - BLOB Storage: Facial encodings (NumPy arrays of type float64) are serialized
    into binary format for database storage.
  - Multi-threaded Access: By setting check_same_thread=False, the system allows
    the Flask API threads to query and update the database simultaneously
    without corruption.

4. Flask REST API & Activity Tracking

The backend is exposed via a Flask web server that manages the application state
and real-time telemetry.

  - State Management: An internal app_state dictionary tracks total scans,
    verified residents, and unknown visitors.
  - Snapshot Serialization: Captured faces are encoded to Base64 strings for
    seamless transmission over JSON to the frontend dashboard.

II- Technical Deep Dive

Face Extraction Logic

margin_y = int(face_height * expand_ratio)
new_t = max(0, t - margin_y)
new_b = min(img_height, b + margin_y)

This specific implementation ensures that even if a visitor is moving, the
bounding box remains robust, significantly reducing the "False Rejection Rate"
(FRR).

Identification Heuristics

The system uses a strict Tolerance Threshold of 0.5. This is a balanced
mathematical trade-off between:

1.  Security (Precision): Preventing unknown users from being identified as
    residents.
2.  Usability (Recall): Ensuring residents are recognized even in varying
    lighting conditions.

III- Installation & Deployment

Prerequisites

  - Python 3.8+
  - cmake (required for face_recognition library)
  - A functional webcam or imaging sensor

Setup

1.  Clone the repository:
    git clone https://github.com/AbderrahmanKM/DoorSense-AI.git
    cd DoorSense-AI
2.  Install dependencies:
    pip install Flask opencv-python face-recognition numpy
3.  Initialize the system:
    python app.py

The dashboard will be available at http://localhost:5000.

IV- The Engineering Team

This project was developed through the collaborative effort of:
  - Abderrahman El Kourrami
  - Ouail Tahiri El Alaoui
  - Labhala Samia
  - Babaida Narjis
  - Zougui Sabir


