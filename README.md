Project Name

SignConnect – Real-Time Sign Language Translator

Definition

SignConnect is a web-based application that uses computer vision and machine learning to recognize sign language gestures through a webcam and convert them into readable text and audible speech, enabling effective communication between hearing-impaired and non-sign-language users.

Objective
To bridge the communication gap between deaf/mute individuals and others.
To translate sign language gestures into text in real time.
To convert recognized text into speech output.
To provide an accessible and user-friendly communication platform.
To promote inclusivity through assistive technology.
```
ER Diagram
+----------------+
|     USER       |
+----------------+
| User_ID (PK)   |
| Name           |
| Email          |
| Password       |
+----------------+
        |
        | Uploads
        |
        v
+----------------+
| GESTURE_DATA   |
+----------------+
| Gesture_ID(PK) |
| User_ID (FK)   |
| Gesture_Name   |
| Image_Path     |
| Date_Time      |
+----------------+
        |
        | Recognized As
        |
        v
+----------------+
| TRANSLATION    |
+----------------+
| Translate_IDPK |
| Gesture_ID(FK) |
| Text_Output    |
| Speech_Output  |
| Accuracy       |
+----------------+
        |
        | Stored In
        |
        v
+----------------+
|     HISTORY    |
+----------------+
| History_ID(PK) |
| User_ID (FK)   |
| Translate_IDFK |
| Date_Time      |
+----------------+
```
Modules
User Registration/Login
Webcam Gesture Capture
Sign Recognition Model
Text Translation
Text-to-Speech Conversion
Translation History
Software Requirements
Python
Flask/FastAPI
OpenCV
MediaPipe
TensorFlow/PyTorch
MySQL
Hardware Requirements
Webcam
4GB+ RAM
Laptop/Desktop
