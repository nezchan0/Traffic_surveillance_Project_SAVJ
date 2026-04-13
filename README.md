# 🚦 Traffic Surveillance Project

A two-server traffic enforcement system that helps traffic officers verify driver and vehicle information quickly using OCR, computer vision, and a centralized MySQL database.

The project has three main parts:

- **Dummy Data Setup** — prepares the MySQL schema and sample records used by the system.
- **Server 1: Django (`DL_Detection`)** — handles driver’s license image upload, OCR extraction, database lookup, and API responses.
- **Server 2: Flask (`Number Plate Detection`)** — monitors live camera input, detects number plates in real time, and fetches vehicle details from Server 1.

---

## 📌 What this project does

This project automates two important traffic enforcement workflows:

1. **Driver’s License Detection**
   - Upload a driver’s license image.
   - Extract details using OCR.
   - Match the extracted data against the database.
   - Show owner, license, vehicle, and face details.

2. **Number Plate Detection**
   - Read live vehicle feed from an IP camera.
   - Detect number plates in real time using a pre-trained YOLO model.
   - Cross-check the plate against the database.
   - Flag suspicious, expired, or wanted records for officers.

---

## 🧱 Repository Structure

```text
Traffic_surveillance_Project/
├── 1_DummyData/
├── 2_DL_Detection_Server1/
├── 3_NumberPlate_Detection_Server2/
└── TrafficSurveillanceProject_Wireframe_ss/
```

### Folder roles

- **`1_DummyData/`**  
  Contains MySQL schema and database import instructions for the sample dataset used by both servers.

- **`2_DL_Detection_Server1/`**  
  Django backend for driver’s license detection, OCR, admin access, and APIs.

- **`3_NumberPlate_Detection_Server2/`**  
  Flask application for live number plate detection and real-time alerts.

- **`TrafficSurveillanceProject_Wireframe_ss/`**  
  Contains architecture diagrams, schema diagram, and UI preview screenshots.

---

## 🧠 High-level architecture

```text
Mobile / IP Camera
        │
        ▼
Flask Server (Number Plate Detection)
        │
        ├── detects plate in live feed
        ├── flags vehicle status
        ▼
Django Server (DL Detection / API Layer)
        │
        ├── database lookup
        ├── vehicle + license data
        ├── face image / suspicious status
        ▼
MySQL Database
```

### How the two servers work together

- **Server 2** continuously watches the road feed.
- When a plate is detected, **Server 2** calls **Server 1** API.
- **Server 1** reads the database and returns the relevant vehicle/driver details.
- The Flask UI displays the result instantly for traffic officers.

---

## ⚙️ Tech Stack

- **Frontend/UI:** Django templates, Flask templates
- **Backend:** Django, Flask
- **Database:** MySQL
- **Computer Vision:** OpenCV, YOLO
- **OCR:** Tesseract OCR
- **Integration:** REST APIs, IP camera stream, ngrok for public tunneling when needed

---

## 🚀 Setup Overview

### 1) Dummy Data
Use the dummy data folder to create and populate the MySQL database.

- Create the database schema
- Insert sample records
- Ensure both servers can query the same dataset

### 2) Server 1 — Django
Server 1 provides:

- Driver’s license image upload
- OCR-based extraction
- Database lookup
- APIs for vehicle details and license details
- Optional Django admin panel for managing records

### 3) Server 2 — Flask
Server 2 provides:

- Live number plate detection
- Real-time vehicle flagging
- Officer-facing monitoring interface
- On-demand fetching of vehicle details from Django

> Both servers should point to the same MySQL database and should be configured with the correct local or ngrok URL when needed.

---

## 🔌 API Flow

### Django API endpoints

- `POST /get_vehicle_details/`
  - Input: number plate
  - Output: vehicle details, suspicious status, face image URL

- `POST /get_data_from_license_image/`
  - Input: license image file
  - Output: owner details, DL details, vehicle details, suspicious person details, face image URL

### Flask integration

- Flask sends the detected number plate to Django.
- Django returns the vehicle and person status.
- Flask shows the status on the monitoring page.

---

## 🎯 Status Color Meaning


- **Green** & **Yellow** → minor felony such as expired PUC
- **Orange** → bad history
- **Red** → wanted currently



---

## 🖼️ Architecture & Schema

### Project Architecture

![Architecture](TrafficSurveillanceProject_Wireframe_ss/Images_Architecture/1_Project_Architecture_Details.png)

### Project Database Schema

![DatabaseSchema](TrafficSurveillanceProject_Wireframe_ss/Images_Architecture/2_TrafficProject_Schema.png)


---

## 📱 DL Detection — Mobile UI Preview

### Landing page

<img src="TrafficSurveillanceProject_Wireframe_ss/Images_DL_detection_Server1_Application/1.DL_Detection_LandingPage.jpg" alt="DL Detection Landing Page" width="100%">

### License details previews

<table>
  <tr>
    <td align="center" width="50%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_DL_detection_Server1_Application/2.DL_Detection_Person1Details_Green.jpg" alt="Person 1 Details Green" width="100%">
      <br><sub>Person 1 — Green</sub>
    </td>
    <td align="center" width="50%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_DL_detection_Server1_Application/3.DL_Detection_Person1DetailsContinued_Green.jpg" alt="Person 1 Details Continued Green" width="100%">
      <br><sub>Person 1 — Continued</sub>
    </td>
  </tr>
  <tr>
    <td align="center" width="50%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_DL_detection_Server1_Application/4.DL_Detection_Person2Details_Orange.jpg" alt="Person 2 Details Orange" width="100%">
      <br><sub>Person 2 — Orange</sub>
    </td>
    <td align="center" width="50%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_DL_detection_Server1_Application/5.DL_Detection_Person2DetailsContinued_Orange.jpg" alt="Person 2 Details Continued Orange" width="100%">
      <br><sub>Person 2 — Continued</sub>
    </td>
  </tr>
  <tr>
    <td align="center" width="50%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_DL_detection_Server1_Application/6.DL_Detection_Person3Details_Red.jpg" alt="Person 3 Details Red" width="100%">
      <br><sub>Person 3 — Red</sub>
    </td>
    <td align="center" width="50%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_DL_detection_Server1_Application/7.DL_Detection_Person3DetailsContinued_Red.jpg" alt="Person 3 Details Continued Red" width="100%">
      <br><sub>Person 3 — Continued</sub>
    </td>
  </tr>
</table>

### Recently accessed persons

<img src="TrafficSurveillanceProject_Wireframe_ss/Images_DL_detection_Server1_Application/8.DL_Detection_Recently_Asscessed_PersonsList.jpg" alt="Recently Accessed Persons List" width="100%">

---

## 🚔 Number Plate Detection — Mobile UI Preview

### Detection flow

<table>
  <tr>
    <td align="center" width="33.33%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_NumberPlate_Detection_Server2_Application/1.NP_Detection_Detecting_1st_flagged_car.jpg" alt="Detecting 1st flagged car" width="100%">
      <br><sub>Detecting 1st flagged car</sub>
    </td>
    <td align="center" width="33.33%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_NumberPlate_Detection_Server2_Application/2.NP_Detection_Detecting_2nd_flagged_car.jpg" alt="Detecting 2nd flagged car" width="100%">
      <br><sub>Detecting 2nd flagged car</sub>
    </td>
    <td align="center" width="33.33%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_NumberPlate_Detection_Server2_Application/3.NP_Detection_Detecting_4th_flagged_car.jpg" alt="Detecting 4th flagged car" width="100%">
      <br><sub>Detecting 4th flagged car</sub>
    </td>
  </tr>
  <tr>
    <td align="center" width="33.33%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_NumberPlate_Detection_Server2_Application/4.NP_Detection_Viewing_FlaggedVechicle_Details_Yellow.jpg" alt="Flagged vehicle details yellow" width="100%">
      <br><sub>Vehicle details — Yellow</sub>
    </td>
    <td align="center" width="33.33%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_NumberPlate_Detection_Server2_Application/5.NP_Detection_Viewing_FlaggedVechicle_Details_Orange.jpg" alt="Flagged vehicle details orange" width="100%">
      <br><sub>Vehicle details — Orange</sub>
    </td>
    <td align="center" width="33.33%">
      <img src="TrafficSurveillanceProject_Wireframe_ss/Images_NumberPlate_Detection_Server2_Application/6.NP_Detection_Viewing_FlaggedVechicle_Details_Red.jpg" alt="Flagged vehicle details red" width="100%">
      <br><sub>Vehicle details — Red</sub>
    </td>
  </tr>
</table>

---

## 🧩 Project Summary

This project combines database-driven verification and real-time computer vision to assist traffic officers in making faster and more reliable decisions.

- **Server 1** focuses on driver identity and document verification.
- **Server 2** focuses on live road monitoring and vehicle flagging.
- **MySQL** acts as the shared data layer.
- The UI is designed for practical, mobile-friendly field usage.

---

## 📎 Notes

- Use the correct local IP or ngrok URL when connecting Server 2 to Server 1.
- Make sure the phone camera and laptop are on the same Wi-Fi network for live stream-based use.
- The same database must be available to both servers.
- Tesseract OCR and YOLO dependencies must be installed correctly for the two detection flows.

---

## ✨ Too cool to miss planning diagrams

The planning-stage diagrams below were created during early design work and are included here as a nice record of the project’s evolution, even though they are not central to the current runtime scope.

### Project Flow Details
![Project Flow Details](TrafficSurveillanceProject_Wireframe_ss/Images_Architecture/0_PlanningStageDetials_Project_Flow_Details.png)

### Planning Stage — Device & Implementation Details
![Planning Stage — Device & Implementation Details](TrafficSurveillanceProject_Wireframe_ss/Images_Architecture/0_PlanningStageDetials_Project_Flow_Details.png)
