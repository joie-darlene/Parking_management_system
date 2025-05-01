Parking Management System
This project is a smart parking gate control system using computer vision and hardware integration. It detects vehicles, reads license plates using OCR, and controls a gate via Arduino based on plate validation.

Features
🚗 Detects vehicles using YOLOv8

🔍 Extracts license plate numbers using Tesseract OCR

🧠 Filters and validates Rwandan plate format (e.g., RA123B)

📊 Saves detected plate logs with timestamps in a CSV file

🚪 Opens/Closes gate using Arduino + Servo motor

📏 Simulates vehicle presence using a mock ultrasonic sensor (can be replaced with real sensor)

Requirements
Python 3.x

Ultralytics YOLOv8

OpenCV

pytesseract

pyserial

Arduino with servo setup

A trained YOLOv8 model (saved as best.pt)

Setup
Install required Python libraries:

bash
Copy
Edit
pip install ultralytics opencv-python pytesseract pyserial
Set the correct Tesseract path in your script:

python
Copy
Edit
pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'
Ensure your Arduino is connected (e.g., COM3). If auto-detection fails, you can manually set it:

python
Copy
Edit
arduino = serial.Serial('COM3', 9600, timeout=1)
Connect your webcam and run the script.

Arduino Note
The Arduino must listen for serial commands '1' (open gate) and '0' (close gate).

Use a simple sketch like:

cpp
Copy
Edit
#include <Servo.h>
Servo gate;
void setup() {
  gate.attach(9);
  Serial.begin(9600);
}
void loop() {
  if (Serial.available()) {
    char command = Serial.read();
    if (command == '1') gate.write(90); // open
    if (command == '0') gate.write(0);  // close
  }
}
Output
Detected plates are saved in plates_log.csv.

Saved images (if enabled) go to the plates/ directory.

Opens the gate only if a valid plate is detected and not recently logged.