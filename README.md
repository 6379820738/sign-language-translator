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

FRONTEND : 
``
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SignConnect - Real Time Sign Language Translator</title>

<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

<style>
body{
    background:#f4f6f9;
}

.navbar{
    background:#0d6efd;
}

.navbar-brand{
    color:white !important;
    font-size:28px;
    font-weight:bold;
}

.card{
    border:none;
    border-radius:15px;
    box-shadow:0px 2px 10px rgba(0,0,0,0.2);
}

video{
    width:100%;
    border-radius:10px;
    border:3px solid #0d6efd;
}

.history-table{
    max-height:250px;
    overflow-y:auto;
}
</style>

</head>
<body>

<nav class="navbar navbar-expand-lg">
<div class="container">
<a class="navbar-brand" href="#">SignConnect</a>
</div>
</nav>

<div class="container mt-4">

<h2 class="text-center mb-4">
Real-Time Sign Language Translator
</h2>

<div class="row">

<div class="col-md-6">

<div class="card p-3">

<h4>Webcam Capture</h4>

<video id="video" autoplay></video>

<button class="btn btn-primary mt-3" onclick="captureGesture()">
Capture Gesture
</button>

</div>

</div>

<div class="col-md-6">

<div class="card p-3">

<h4>Translation Output</h4>

<label>Recognized Gesture</label>

<input
type="text"
class="form-control mb-3"
id="gesture"
readonly>

<label>Translated Text</label>

<textarea
class="form-control"
rows="4"
id="translatedText"
readonly></textarea>

<label class="mt-3">Accuracy</label>

<input
type="text"
class="form-control"
id="accuracy"
readonly>

<button
class="btn btn-success mt-3"
onclick="speakText()">
Speak
</button>

</div>

</div>

</div>

<div class="card p-3 mt-4">

<h4>Translation History</h4>

<div class="history-table">

<table class="table table-bordered">

<thead class="table-primary">
<tr>
<th>Gesture</th>
<th>Text</th>
<th>Accuracy</th>
</tr>
</thead>

<tbody id="historyBody">

</tbody>

</table>

</div>

</div>

</div>

<script>

const sampleData = [
{
gesture:"HELLO",
text:"Hello",
accuracy:"98%"
},
{
gesture:"THANK YOU",
text:"Thank You",
accuracy:"97%"
},
{
gesture:"YES",
text:"Yes",
accuracy:"96%"
},
{
gesture:"NO",
text:"No",
accuracy:"95%"
},
{
gesture:"WELCOME",
text:"Welcome",
accuracy:"99%"
}
];

navigator.mediaDevices.getUserMedia({
video:true
})
.then(stream=>{
document.getElementById("video").srcObject=stream;
})
.catch(error=>{
alert("Webcam Access Denied");
});

function captureGesture(){

const random =
sampleData[Math.floor(
Math.random()*sampleData.length
)];

document.getElementById("gesture").value =
random.gesture;

document.getElementById("translatedText").value =
random.text;

document.getElementById("accuracy").value =
random.accuracy;

addHistory(random);
}

function speakText(){

const text =
document.getElementById(
"translatedText"
).value;

if(text===""){
alert("No Text Available");
return;
}

const speech =
new SpeechSynthesisUtterance(text);

window.speechSynthesis.speak(speech);
}

function addHistory(data){

const row = `
<tr>
<td>${data.gesture}</td>
<td>${data.text}</td>
<td>${data.accuracy}</td>
</tr>
`;

document.getElementById("historyBody")
.innerHTML += row;
}

</script>

</body>
</html>
``
