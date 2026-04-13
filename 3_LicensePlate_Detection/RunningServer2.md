# 🚦 Traffic Surveillance - Server 2 (Number Plate Detection) - Setup guide

Follow the steps below to set up and run the Server 2 properly.

------------------------------------------------------------------------

## 🐍 Step 1: Create Virtual Environment

Create a virtual environment:

``` bash
python -m venv venv
venv\Scripts\activate
```

-   This will isolate dependencies for the Flask application.

------------------------------------------------------------------------

## 📦 Step 2: Install Dependencies

Install all required packages:

``` bash
pip install -r requirements.txt
```

------------------------------------------------------------------------

## ⚙️ Step 3: Configure Server Code

Update the following variables in your Flask script:

### 🔧 1. Django Server (Server 1 URL)

``` python
BaseURL = "http://127.0.0.1:8000"
# BaseURL = "https://your-ngrok-url.ngrok-free.app"
```

-   This should point to Server 1 (DL Detection - Django)

------------------------------------------------------------------------

### 🔧 2. API Endpoint

``` python
APISITEURL = f"{BaseURL}/TrafficProject/api/vehicle-details/"
```

------------------------------------------------------------------------

### 🔧 3. IP Camera URL

``` python
video_source = "https://<your-phone-ip>:8080/video"
```

⚠️ VERY IMPORTANT: - Mobile phone (camera) and laptop (Flask server)
MUST be on the same WiFi network

------------------------------------------------------------------------

## 🌐 Step 4: Network Configuration

### 🏠 Case 1: Same Network (Localhost Setup)

-   http://127.0.0.1:8000 (Django)
-   http://127.0.0.1:5000 (Flask)

------------------------------------------------------------------------

### 🌍 Case 2: Different Networks (Using Ngrok)

``` bash
ngrok http 8000
```

``` python
BaseURL = "https://your-ngrok-url.ngrok-free.app"
```

------------------------------------------------------------------------

## 📡 Step 5: Important Links

-   Django Backend → `http://<laptop-ip>:8000`
-   Flask App → `http://<laptop-ip>:5000`
-   IP Camera → `http://<phone-ip>:8080/video`

------------------------------------------------------------------------

## ▶️ Step 6: Run the Server

``` bash
python main.py
```

------------------------------------------------------------------------

## 🖥️ Step 7: Frontend Interface

Open the following on a user phone (ensure phone and laptop are on the same WiFi):

    http://<laptop-ip>:5000/

### 🚔 What this interface does:

- Provides a **live camera feed** from the IP camera  
- Designed for **real-time monitoring (e.g., police usage)**  

- Whenever a vehicle is detected and flagged by the Flask server:
  - Its **details are instantly fetched from Django backend**
  - Displayed immediately on the interface  

- This allows officers to:
  - View the **vehicle number**
  - See **suspicious/felony details**
  - Take **immediate action (e.g., stop the vehicle)**  

- UI also supports:
  - Click to view **full vehicle + owner details**
  - Face image display for quick identification

------------------------------------------------------------------------

## 📱 Step 8: Usage Flow

1.  Start Django Server
2.  Start Flask Server
3.  Open Flask UI 
4.  Ensure camera stream works

------------------------------------------------------------------------

## ⚠️ Important Notes

-   Both servers must run together
-   Correct API URL must be set
-   YOLO model file required
-   Same WiFi required

------------------------------------------------------------------------

## ✅ Final Checklist

-   Virtual env ✔️
-   Dependencies ✔️
-   API configured ✔️
-   Camera working ✔️
-   Detection running ✔️

------------------------------------------------------------------------
