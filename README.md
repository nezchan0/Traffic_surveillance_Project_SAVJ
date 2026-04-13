# 🚦 Traffic Detection System - Full Project Overview

This project consists of two integrated systems:

1. **Django Backend (Traffic Project)**
2. **Flask Real-Time License Plate Detection Server**

Together, they form a complete pipeline for detecting vehicle license plates and retrieving associated data in real time.

---

## 🧠 Project Architecture Overview

```
[📱 Camera Phone] ---> [🖥️ Flask Detection Server] ---> [🌐 Django Backend] ---> [📱 User Phone]
         |                        |                           |                      |
     Video Feed            Plate Detection            Data Fetch API          UI Display
```

---

## 🔹 1. Django Backend (Traffic Project)

### 📌 Purpose

* Stores vehicle and license data
* Provides API to fetch vehicle details
* Admin panel to manage records

### ⚙️ Key Features

* REST API for vehicle lookup
* MySQL database integration
* Admin dashboard
* Dummy data import system

### 🌐 Runs On

* Port **8000**

---

## 🔹 2. Flask Detection Server

### 📌 Purpose

* Captures live video stream
* Detects license plates using YOLO
* Extracts text using EasyOCR
* Sends detected plates to frontend & Django backend

### ⚙️ Key Features

* Real-time detection
* SSE (Server-Sent Events) for live updates
* Multiprocessing for performance
* Integration with Django API

### 🌐 Runs On

* Port **5000**

---

## 📡 System Flow

1. 📱 Camera phone streams video (IP Webcam)
2. 🖥️ Flask server:

   * Captures video
   * Detects number plates (YOLO)
   * Extracts text (OCR)
3. 🔗 Detected plate is sent to Django API
4. 🌐 Django returns vehicle details
5. 📱 User views results in real-time

---

## 🔗 Required Links

* **Django Backend (Link 1)** → `http://<laptop-ip>:8000`
* **Flask Server (Link 2)** → `http://<laptop-ip>:5000`
* **Video Feed (Link 3)** → `http://<phone-ip>:8080/video`

---

## 📶 Network Requirement

All devices must be connected to the **same WiFi network**:

* 💻 Laptop → Runs Django + Flask
* 📱 Phone 1 → Camera (IP Webcam)
* 📱 Phone 2 → User Interface

---

## ▶️ How to Run (High Level)

### Step 1: Start Django Backend

```bash
python manage.py runserver
```

### Step 2: Start Flask Server

```bash
python app.py
```

---

## 📱 Usage Order (Important)

On the **user phone**, follow this order:

1. Open **Django Backend (Link 1)**
2. Open **Video Feed (Link 3)**
3. Open **Flask Server (Link 2)**

---

## ⚠️ Configuration Checklist

* Update **IP addresses** in Flask code
* Ensure **YOLO model file (`license_plate_detector.pt`) is present**
* Install all dependencies
* Configure database in Django
* Import dummy data

---

## ✅ Final Outcome

* Live video stream processed ✔️
* License plate detected ✔️
* Data fetched from backend ✔️
* Results displayed on user phone ✔️

---

## 🚀 Tech Stack

* **Backend**: Django, Django REST Framework
* **Detection Server**: Flask
* **Computer Vision**: OpenCV, YOLO (Ultralytics)
* **OCR**: EasyOCR, PyTorch
* **Database**: MySQL
* **Frontend**: HTML / JavaScript (SSE-based)

---

## 📌 Notes

* ❗ Do NOT use `localhost` when accessing from phone → use local IP
* Ensure ports **8000** and **5000** are open
* Use `use_reloader=False` in Flask (required for multiprocessing)
* All devices must be on the same WiFi network

---

## 🎯 Summary

This project simulates a **real-time traffic monitoring system**:

* Detects vehicles using camera feed
* Extracts license plate numbers
* Fetches vehicle details from backend
* Displays everything live on a mobile device
