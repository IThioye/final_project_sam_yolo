# SAM2 + YOLO : Image Annotation and Image Classification for void and components in printed circuit board

## Overview
SAM2 is a powerful image and video segmentation framework developed by Meta Platforms, Inc. It enables users to perform segmentation tasks on images and videos. This repository provides a Flask web application that allows users to upload chip images, generate masks, classify components, and retrain models.

## Features
- Upload images for segmentation using SAM
- Generate masks for images and visualize results
- Classify images and obtain area statistics for components
- Retrain the YOLO model with new datasets
- Real-time updates through WebSocket for training progress

## Requirements
- Python 3.11+
- Flask
- Flask-SocketIO
- OpenCV
- NumPy
- Matplotlib
- PyTorch
- Ultralytics YOLO
- Segment Anything Model 2 (SAM2)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/IThioye/final_project_sam_yolo.git
```

2. Install the required packages:
```bash
pip install -r requirements.txt
```

## Configuration
The configuration for the application can be found in `app.py`. You can adjust the following parameters:
- `UPLOAD_FOLDER`: Directory for uploaded images
- `SAM_RESULT_FOLDER`: Directory for saving SAM results
- `YOLO_RESULT_FOLDER`: Directory for saving YOLO results
- Model paths for YOLO and SAM


## Usage

1. Start the Flask application:
```bash
python app.py
```

2. Open your web browser and navigate to `http://127.0.0.1:5001/`

3. Use the web interface to:
   - Upload images for segmentation
   - Generate masks and visualize results
   - Classify images and retrieve area statistics
   - Retrain the YOLO model with new datasets


## API Endpoints

### POST /upload_sam
Upload an image for SAM segmentation.

**Request:**
- Method: POST
- Content-Type: multipart/form-data
- Body: file (image file)

**Response:**
```json
{
    'message': 'File uploaded successfully',
    'image_url': image_url,
    'filename': filename,
    'dimensions': {
        'width': width,
        'height': height
}
```

### POST /upload_yolo
Upload an image for YOLO processing.

**Request:**
- Method: POST
- Content-Type: multipart/form-data
- Body: file (image file)

**Response:**
```json
{
    'message': 'File uploaded successfully',
    'image_url': image_url,
    'filename': filename
}
```

### POST /generate_mask
Generate masks for a given image.

**Request:**
- Method: POST
- Content-Type: application/json
- Body:
```json
{
    "filename": the name of the image file,
    "normalized_void_points": a list of normalized 2D points (x, y) representing the voids,
    "normalized_component_boxes": a list of normalized 2D bounding boxes (x, y, w, h) representing the components
}
```

**Response:**
```json
{
    'status': 'success',
    'train_image_url':the URL of the saved train image,
    'result_path': the URL of the saved result image
}
```

### POST /classify
Classify an image and return results.

**Request:**
- Method: POST
- Content-Type: application/json
- Body:
```json
{
    "filename": the name of the image file
}
```

**Response:**
```json
{
    'status': 'success',
    'result_path': URL of the annotated image,
    'area_data': a list of dictionaries containing the area and overlap statistics for each component,
    'area_data_path': URL of the JSON file containing the area data
}
```

### POST /start_retraining
Start the retraining process for YOLO.

**Request:**
- Method: POST
- Content-Type: application/json


## Project Structure
```
final_project_sam_yolo/
├── app.py
├── requirements.txt
├── sam2/
├── static/
│   ├── sam/
│        ├── sam_results/
│        └── sam2.1_hiera_tiny.pt
│   ├── yolo/
│        ├── area_data
│        ├── dataset_yolo
│        ├── yolo_results
│        └── model_yolo.pt
│   └── uploads/
├── templates/
│   ├── index.html
│   ├── yolo.html
│   └── retrain.html

```

## Contact
For any inquiries, please contact [ibou2003@gmail.com]