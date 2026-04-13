# 🚦 Traffic Surveillance - Server 1 (DL_Detection) - Setup guide

Follow the steps below to set up and run the server1 properly.

------------------------------------------------------------------------

## 🐍 Step 1: Create Virtual Environment

Create a virtual environment .

``` bash
python -m venv myevn
myevn\Scripts\activate
```

-   This will create and activate a Python virtual environment in your
    project directory.

------------------------------------------------------------------------

## 📦 Step 2: Install Dependencies

Install all required packages:

``` bash
pip install -r requirements.txt
```

------------------------------------------------------------------------

## 🔍 Step 3: Install Tesseract OCR

-   Install the **Tesseract Engine** on your system.
-   Update the correct configuration path in:

```
server1/TrafficProject/myapp/utils/extract_license_number_from_image.py

```
    
------------------------------------------------------------------------

## ⚙️ Step 4: Configure Database

-   Open `settings.py`
-   Update database configurations (around **line 81**) according to
    your system setup.

------------------------------------------------------------------------

## 🗂️ Step 5: Add Dummy Data

Before running the server1, populate the database using instruction given in this file:

    Traffic_surveillance_Project_SAVJ/1_DummyData/Importing_Dummy_Data.md

------------------------------------------------------------------------

## 🧱 Step 6: Run Migrations

Navigate to the project directory:

``` bash
cd server1/TrafficProject
```

Run the following commands:

``` bash
python manage.py makemigrations
python manage.py migrate
```

> These commands ensure all database migrations are applied.

------------------------------------------------------------------------

## ▶️ Step 7: Run the Server

Start the Django development server:

``` bash
python manage.py runserver
```

------------------------------------------------------------------------


## 🔐 Step 8: Create Admin User (Optional)

To access Django admin panel:

``` bash
python manage.py createsuperuser
```

-   Create user and password.

-   You can view and manage database data from the admin interface.
------------------------------------------------------------------------

## 🌐 Step 9: Frontend + API Usage

This Django server provides **two functionalities**:

### 1. 🖥️ Frontend Interface (Django Templates)

-   Built using **Django templates**
-   Users can:
    -   Upload a **Driving License image**
    -   View extracted **person details, vehicle info, and face image**
-   Access it via browser on Base SiteUrl (localhost 8000 or ngrok hosted link):


------------------------------------------------------------------------

### 2. 🔌 Backend APIs

The server exposes **2 APIs**:

#### 📌 API 1: Get Vehicle Details (used by Server 2 - Number Plate Detection)

``` python
POST /get_vehicle_details/
{
  "numberplate": "TN01AB1234"
}
```

-   Returns:
    -   Vehicle details
    -   Suspicious vehicle details
    -   Face image URL

------------------------------------------------------------------------

#### 📌 API 2: Extract & Get Data from License Image

``` python
POST /get_data_from_license_image/
FormData:
  dl_image: <image file>
```

-   Returns:
    -   Owner details
    -   DL details
    -   Vehicle details
    -   Suspicious person details
    -   Face image URL

------------------------------------------------------------------------

### 🌍 Important (Ngrok Usage for Server 2 Integration)

Since **Server 2 (Number Plate Detection)** will consume this API:

-   You can expose this Django server using **ngrok**

#### 👉 If using ngrok:

``` python
SITE_URL = "https://your-ngrok-url.ngrok-free.app"
```

#### 👉 If running locally:

``` python
SITE_URL = "http://127.0.0.1:8000"
```

> This is important because APIs return image URLs using `SITE_URL`. 

> 'SITE_URL' can be changed in settings.py ( around line 148 )



------------------------------------------------------------------------

## ✅ Final Checklist

-   Virtual environment created & activated ✔️\
-   Dependencies installed ✔️\
-   Tesseract configured ✔️\
-   Database configured ✔️\
-   Dummy data added ✔️\
-   Migrations applied ✔️\
-   Server running ✔️\
-   Frontend + APIs working ✔️

------------------------------------------------------------------------
