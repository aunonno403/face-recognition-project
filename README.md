# Face Recognition Attendance System

A real-time face recognition-based attendance system that uses OpenCV and KNN classifier to capture, recognize, and record attendance automatically.

## Features

- **Face Data Collection**: Capture and store face data with associated names
- **Real-time Face Recognition**: Recognize faces using K-Nearest Neighbors (KNN) algorithm
- **Automated Attendance**: Record attendance with timestamp in CSV format
- **Voice Feedback**: Audio confirmation when attendance is taken
- **Web Dashboard**: Streamlit-based dashboard to view attendance records with auto-refresh

## Requirements

```
opencv-python (cv2)
numpy
scikit-learn
streamlit
streamlit-autorefresh
pandas
pywin32
pickle (built-in)
```

## Installation

1. Clone or download this repository

2. Install required packages:
```bash
pip install opencv-python numpy scikit-learn streamlit streamlit-autorefresh pandas pywin32
```

3. Ensure you have the Haar Cascade classifier file:
   - Place `haarcascade_frontalface_default.xml` in the `data/` directory
   - You can download it from [OpenCV GitHub repository](https://github.com/opencv/opencv/tree/master/data/haarcascades)

4. Create necessary directories:
```bash
mkdir data
mkdir Attendance
```

5. (Optional) Add a `background.png` file for the test interface

## Project Structure

```
face_recognition_project/
│
├── add_faces.py              # Script to capture and store face data
├── test.py                   # Face recognition and attendance recording
├── app.py                    # Streamlit dashboard for viewing attendance
├── data/
│   ├── haarcascade_frontalface_default.xml
│   ├── names.pkl             # Stored names (generated automatically)
│   └── faces_data.pkl        # Stored face data (generated automatically)
├── Attendance/               # CSV attendance files (generated automatically)
└── background.png            # (Optional) Background image for test.py
```

## Usage

### 1. Adding Face Data (`add_faces.py`)

This script captures face images and stores them for training.

```bash
python add_faces.py
```

- Enter your name when prompted
- Look at the camera; the system will capture 100 face images
- Press `q` to quit early or wait until 100 images are captured
- Data is saved to `data/names.pkl` and `data/faces_data.pkl`

### 2. Running Face Recognition & Attendance (`test.py`)

This script recognizes faces and records attendance.

```bash
python test.py
```

- The webcam will start and detect faces in real-time
- Recognized names will be displayed on the video frame
- Press `o` to record attendance for the detected person
- Voice feedback confirms "Attendance Taken"
- Press `q` to quit
- Attendance is saved in `Attendance/Attendance_DD-MM-YYYY.csv`

### 3. Viewing Attendance Dashboard (`app.py`)

Launch the Streamlit dashboard to view attendance records.

```bash
streamlit run app.py
```

- Opens a web interface (usually at http://localhost:8501)
- Displays attendance for the current date
- Auto-refreshes every 2 seconds
- Highlights maximum values in the dataframe

## How It Works

1. **Face Detection**: Uses Haar Cascade Classifier to detect faces in video frames
2. **Feature Extraction**: Crops and resizes detected faces to 50x50 pixels
3. **Training**: Stores face data and uses KNN classifier for recognition
4. **Recognition**: Compares detected faces with stored data (k=5 neighbors)
5. **Attendance Logging**: Records name and timestamp in CSV files organized by date

## Notes

- Ensure good lighting conditions for better face detection
- Look directly at the camera when capturing face data
- Each person should capture at least 100 face samples for better accuracy
- The system uses 5-nearest neighbors for classification (adjustable in `test.py`)
- Attendance files are organized by date in DD-MM-YYYY format

## Troubleshooting

- **Camera not opening**: Check if another application is using the webcam
- **No faces detected**: Ensure proper lighting and face the camera directly
- **Recognition accuracy issues**: Capture more diverse face angles during training
- **File not found errors**: Verify the `data/` and `Attendance/` directories exist

## License

Free to use for educational and personal projects.
