
# S.T.A.L.K. (SMART TRACKING & ALERT for LEOPARD KINETICS)

## 📌 Project Overview

The S.T.A.L.K. project is a proactive, AI-powered real-time leopard detection system designed to manage and mitigate human-wildlife conflicts in rural and semi-urban areas bordering forested regions. By integrating computer vision with an automated early-warning mechanism, the system detects leopards via camera feeds and immediately dispatches SMS alerts containing geographic location details to relevant authorities and local communities.

## ⚠️ The Problem

**Habitat Encroachment:** Deforestation and human encroachment into natural habitats have forced leopards into populated areas in search of food and territory.


**Fatal Incidents:** There has been an increase in fatal leopard attacks and injuries in regions like Junnar (Maharashtra), Sheopur (Madhya Pradesh), and Bahraich (Uttar Pradesh) .


**Need for Early Warning:** Traditional monitoring methods are often delayed. An affordable, real-time warning system is urgently needed to give people time to stay safe and to prevent retaliatory killings of wildlife.



## ✨ Key Features

*
**Real-Time Detection:** Utilizes the YOLOv5 object detection model for high-speed and accurate identification of leopards through a standard webcam feed.


*
**Automated SMS Alerts:** Integrates with the Twilio API to automatically send SMS alerts with location coordinates the moment a leopard is detected.


*
**Lightweight & Deployable:** Designed to run on standard hardware without requiring high-end surveillance infrastructure, making it scalable for field deployment in remote areas.


*
**Robust Dataset:** Trained on a unified dataset combining real leopard images from diverse environments and custom augmentations to ensure high performance.



## 🛠️ Technology Stack

*
**Machine Learning Model:** YOLOv5 (PyTorch framework)


*
**Dataset Management & Annotation:** Roboflow


*
**Model Training Environment:** Google Colab (GPU)


*
**Programming Languages & Libraries:** Python, OpenCV


*
**Alert Integration:** Twilio API



## 🚀 Setup & Installation

### 1. Environment Setup

Clone the YOLOv5 repository and install the necessary dependencies:

```bash
[cite_start]git clone https://github.com/ultralytics/yolov5 [cite: 501]
[cite_start]cd yolov5 [cite: 502]
[cite_start]pip install roboflow [cite: 504]
[cite_start]pip install -r requirements.txt [cite: 505]

```

### 2. Dataset Integration

The dataset is managed via Roboflow and can be downloaded using the API:

```python
[cite_start]from roboflow import Roboflow [cite: 485]
[cite_start]rf = Roboflow(api_key="YOUR_API_KEY") [cite: 486]
[cite_start]project = rf.workspace("your-workspace").project("leopard-detection") [cite: 487]
[cite_start]dataset = project.version(x).download("yolov5") [cite: 488]

```

### 3. Model Training

The model is trained using the `yolov5s` (small) architecture:

```bash
[cite_start]python train.py --img 640 --batch 16 --epochs 50 --data dataset/data.yaml --weights yolov5s.pt --name leopard_model [cite: 527-534]

```

### 4. Alert System Integration

Configure the Twilio API in your Python script to enable SMS alerts:

```python
[cite_start]from twilio.rest import Client [cite: 574]

[cite_start]account_sid = 'your_account_sid' [cite: 575]
[cite_start]auth_token = 'your_auth_token' [cite: 575]
[cite_start]client = Client(account_sid, auth_token) [cite: 576]

[cite_start]def send_sms_alert(to_number): [cite: 577]
    [cite_start]message_body = ( [cite: 578]
        [cite_start]"Leopard Detected!\n\n" [cite: 581]
        [cite_start]"Location: https://www.google.com/maps?q=18.531669,73.867227\n\n" [cite: 582]
        [cite_start]"Please respond immediately." [cite: 583]
    )
    [cite_start]client.messages.create( [cite: 584]
        [cite_start]body=message_body, [cite: 585]
        [cite_start]from_='+1234567890', [cite: 586]
        [cite_start]to=to_number [cite: 587]
    )

[cite_start]if leopard_detected: [cite: 589]
    [cite_start]recipient_number = '+919876543210' [cite: 590]
    [cite_start]send_sms_alert(recipient_number) [cite: 591]

```

## 🚧 Challenges Overcome

*
**Dataset Standardization:** Cleaned and standardized inconsistent dataset labels (e.g., merging "big_cat" or "panthera" into "leopard") and manually corrected bounding boxes for camouflaged subjects .


*
**Resource Constraints:** Managed Google Colab GPU session timeouts by training in smaller batches and utilizing Google Drive for checkpoint backups .


*
**Hardware Integration:** Debugged standard webcam integration permissions and optimized Python processing overhead to minimize video feed lag during real-time detection .



## 🔮 Future Scope

* Expand the model to detect multiple animal species for broader wildlife threat management.


* Improve night-time detection reliability using infrared or thermal cameras.


* Integrate GPS modules for precise location-based tracking and history logging.


* Develop a dedicated mobile app or user dashboard for streamlined monitoring by forest officials.


