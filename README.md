# Swift-YOLO Training Notebook for Grove Vision AI V2

## Overview

This Google Colab notebook provides a complete training pipeline for deploying a Swift-YOLO object detection model optimized for the **Grove Vision AI V2** module. Train custom models with your own dataset and deploy them to the SenseCraft AI platform.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1exwCxg9p6a-RkrHwSvF65KMXGjGvV-68?usp=sharing)

## Key Features

- **Swift-YOLO Architecture**: Based on YOLOv5, optimized for edge devices
- **192x192 Input Size**: Optimized resolution for Grove Vision AI V2
- **INT8 Quantization**: Full integer quantization for NPU acceleration
- **Vela Compilation**: Automatic conversion to `int8_vela.tflite` format
- **SenseCraft Integration**: Direct deployment to [SenseCraft AI platform](https://sensecraft.seeed.cc/ai/model)

## Prerequisites

- Google Colab account
- Roboflow account with labeled dataset
- Grove Vision AI V2 hardware (for deployment)
- SenseCraft account

## Quick Start Guide

### Step 1: Prepare Your Dataset in Roboflow

1. **Label your dataset** in [Roboflow](https://app.roboflow.com/)
2. **Export your dataset**:
   - Navigate to your project → `Versions` → `Train` → `Download Dataset`
   - Under `Image and Annotation Format`, select **`COCO`**
   - Click `Show download code` and then `Continue`
   - Select **`Jupyter`** as the format
3. **Copy the project code**:
   - Copy the 3rd line that looks like: `project = rf.workspace("xxx-xxx").project("xxx")`
   - You'll paste this into the Colab notebook in the next step

### Step 2: Configure Roboflow API Key in Colab

1. Go to your [Roboflow Settings](https://app.roboflow.com/settings/api)
2. Copy your private API key
3. In Colab, click the **key icon** (🔑) on the **left sidebar** to open Secrets
4. Add a new secret:
   - **Name**: `ROBOFLOW_API_KEY`
   - **Value**: Your API key
5. **Grant access**: Make sure you give the notebook access to the secret key

### Step 3: Run the Colab Notebook

1. **Open the notebook**: [Click here to open in Colab](https://colab.research.google.com/drive/1exwCxg9p6a-RkrHwSvF65KMXGjGvV-68)

2. **Enable GPU Acceleration**:
   - Click `Runtime` → `Change runtime type`
   - Select `GPU` in `Hardware accelerator`
   - Click `Save`

3. **Configure your dataset**:
   - Find the code block marked: `⚠️ PASTE YOUR PROJECT CODE LINE IN THE CODE BLOCK BELOW`
   - Paste your Roboflow project code line (from Step 1)
   - Adjust the version number if needed (default is 1)

4. **Run all cells**: Execute the notebook cells in order

5. **Verify environment** (first cell output should show):
   - GPU: T4 or higher
   - Python 3.11.13

### Step 4: Deploy to SenseCraft AI

1. After training completes, download your model from Colab
2. Go to [SenseCraft AI platform](https://sensecraft.seeed.cc/ai/model)
3. Click `My Own Models` → `+ Add Model`
4. Follow the upload instructions
5. Download the final `int8_vela.tflite` model for deployment

## Model Requirements

### Input Specifications
- **Image Size**: 192x192 pixels (square)
- **Format**: RGB
- **Annotation Format**: COCO JSON

### Output Format
- **File Extension**: `*_int8_vela.tflite` (required)
- **File Size**: Maximum 2.4 MB
- **Quantization**: INT8

## Troubleshooting

### Common Issues

1. **"Invoke failed" Error**
   - **Cause**: Model not in `int8_vela.tflite` format
   - **Solution**: Ensure Vela compilation step completed successfully in the notebook
   - **Reference**: [Troubleshooting Guide](https://wiki.seeedstudio.com/grove_vision_ai_v2_sscma/#:~:text=of%20your%20improvements.-,2,-.%20Why%20do%20I)

2. **Model Size Too Large**
   - **Limit**: 2.4 MB maximum
   - **Solution**: Reduce model complexity or ensure proper quantization

3. **Image Size Mismatch**
   - **Requirement**: Must be 192x192 pixels
   - **Solution**: Configure Roboflow preprocessing to resize images to 192x192

4. **API Key Not Found**
   - **Solution**: Verify the secret is named exactly `ROBOFLOW_API_KEY` and notebook has access
   - **Notebook has no access**: Ensure that the toggle switch next to the key labeled `ROBOFLOW_API_KEY` is set to "on" to provide the Colab notebook with access.

5. **Dataset Download Fails**
   - **Solution**: Verify your project code line is correct and version number exists

## Additional Resources

- **Grove Vision AI V2 Documentation**: [Seeed Studio Wiki](https://wiki.seeedstudio.com/grove_vision_ai_v2_sscma/)
- **Roboflow Documentation**: [Roboflow Help Center](https://docs.roboflow.com/)
- **SenseCraft AI Platform**: [SenseCraft AI](https://sensecraft.seeed.cc/ai/model)

## Notes

- The notebook automatically handles Vela compilation for Ethos-U55 NPU optimization
- Models are optimized for Grove Vision AI V2 hardware constraints
- Training time depends on dataset size and GPU availability




