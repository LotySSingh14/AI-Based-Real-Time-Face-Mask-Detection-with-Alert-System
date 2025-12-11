# AI-Based-Real-Time-Face-Mask-Detection-with-Alert-System
AI-based real-time Face Mask Detection system using Deep Learning and OpenCV. Detects “Mask / No Mask” from webcam feed and triggers an alert for safety monitoring.
Objective:

The project detects whether a person in front of the webcam is wearing a mask or not.
If a person is without a mask, it triggers an alert sound, draws a red bounding box, and saves a violation image in a folder.
If a person is with a mask, it shows a green bounding box and stops the alert.
It also keeps track of the total number of violations.
This can be used in public places, offices, or schools to enforce mask compliance during pandemics.

Technologies & Libraries Used:

1. OpenCV (cv2)
For capturing webcam feed.
For face detection (Haar Cascade Classifier).
For drawing bounding boxes and displaying results.

2. PyTorch (torch)
For running the deep learning model.
Loads a Swin Transformer model to classify mask/no-mask faces.

3. Transformers (Hugging Face)
AutoImageProcessor – preprocesses face images before giving them to the model.
SwinForImageClassification – a Vision Transformer model trained for image classification.

4. PIL (Python Imaging Library)
For image preprocessing (resizing the cropped face to 224×224).

5. Pygame
To play alert sounds when a violation occurs.

6. Datetime & OS
For saving violation images with timestamped filenames in the "violations" folder.

7. Haar Cascade Classifier
A pre-trained face detector from OpenCV.

How It Works (Step-by-Step):

1. Setup
Initializes pygame for alert sound.
Loads the trained mask detection model (./model).
Moves model to GPU (cuda) if available, otherwise CPU.
Loads the Haar cascade classifier to detect faces in the video.
Creates a folder named "violations" to save images.

2. Webcam Input
Opens the webcam using cv2.VideoCapture(0).
Continuously reads frames in a loop.

3. Face Detection
Converts each frame into grayscale (needed for Haar cascade).
Detects faces in the frame → returns bounding boxes (x, y, w, h).

4. Face Classification
For each detected face:
Crop the face region.
Resize it to 224×224 pixels.
Preprocess using Hugging Face processor.
Pass through the Swin Transformer model.
Get the predicted label → "With Mask" or "Without Mask".

5. Violation Handling
If without mask:
Draw a red box around the face.
Play an alert sound (only if not already playing).
Save the violation frame into the violations folder, but only if the last violation was more than 5 seconds ago (cooldown).
If with mask:
Draw a green box.
Stop the alert sound if playing.
If uncertain/other:
Draw a yellow box.

6. Tracking Violations
Maintains a violation counter.
Displays the total count at the top-left corner of the screen.

7. Output Display
Shows the live video with:
Bounding boxes around faces.
Labels ("With Mask" / "Without Mask").
Violation count in red.

8. Exit
Press q to quit the program.
Releases webcam, closes OpenCV windows, and quits pygame.

Project Structure
project/
│── model/                # Pretrained Swin Transformer model & processor
│── alert.wav             # Alert sound file
│── violations/           # Auto-created folder for saving violation frames
│── mask_detection.py     # Your code file

Example Flow:
1. Person comes in front of the webcam.
2. Face detected → cropped and sent to model.
3. Model predicts:
"With Mask" → Green box, no alert.
"Without Mask" → Red box, alert sound, image saved.
4. System displays violation count on screen.
5. If multiple violations occur, system saves multiple images (but ensures cooldown of 5s).

Features:
Real-time detection with bounding boxes.
Automatic alert system with sound.
Saves violation images with timestamp.
Tracks total violations.
Uses AI model (Swin Transformer) for classification.

Possible Enhancements:
Add a database/log file to store violation history.
Send email or SMS alerts to security team.
Extend to multiple persons detection simultaneously.
Integrate with CCTV footage instead of just webcam.
Add GUI/web dashboard for monitoring.

In short:
This project combines Computer Vision (OpenCV), AI (Swin Transformer), and Alert Mechanism (pygame) to build a real-time Face Mask Detection & Violation Alert System.


















