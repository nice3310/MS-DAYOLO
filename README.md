
# MS-DAYOLO

This repository provides a compiled version of **MS-DAYOLO** for Windows 10, based on the original project:  
[GitHub - Mazin-Hnewa/MS-DAYOLO](https://github.com/Mazin-Hnewa/MS-DAYOLO)

---

## Prerequisites

Here's something must install, please follow **Preparation Steps**:

- **Visual Studio** 2017 or 2019 (for CUDA Toolkit 10.1 installation)
- **Windows 10**
- **OpenCV** 4.9
- **CUDA Toolkit** 10.1
- **cuDNN** 7.6.5 (compatible with CUDA 10.1)

---

## Preparation Steps

### 1. Install Visual Studio

Download and install **Visual Studio 2017 or 2019** with the **Desktop Development with C++** workload.  
👉 [Visual Studio 2019 Release Notes](https://learn.microsoft.com/en-us/visualstudio/releases/2019/history#release-dates-and-build-numbers)

---

### 2. Install CUDA Toolkit 10.1

Download and install **CUDA Toolkit 10.1** from the [CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive).  
> **Note**: Make sure Visual Studio is installed first.

---

### 3. Set Environment Variables

Add the following system environment variables:

| **System Variable** | **Value**                                                                 |
|----------------------|---------------------------------------------------------------------------|
| `CUDA_PATH`          | `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.1`              |
| `CUDA_PATH_V10_1`    | `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.1`              |

Update the `Path` environment variable by adding these entries:

| **Path**                                                                 |
|--------------------------------------------------------------------------|
| `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.1\bin`          |
| `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.1\libnvvp`      |

---

### 4. Verify CUDA Installation

Open a **Command Prompt** and run the following command to verify the installation:

```cmd
nvcc --version
```

You should see output similar to this:  
![Verification Example](https://github.com/user-attachments/assets/82089400-5e4f-4049-b6ab-ac3a7659a43d)

---

### 5. Install cuDNN 7.6.5

Download **cuDNN 7.6.5** for CUDA 10.1 from the [cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive).  
After extraction, you should see files like this:  
![cuDNN Files](https://github.com/user-attachments/assets/c94dd384-1848-4e83-9bb1-5e7c92638f38)

Copy the files to their respective directories in your CUDA installation path (`C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.1`):

| **cuDNN File**               | **Target Directory**                                      |
|-------------------------------|----------------------------------------------------------|
| `bin\cudnn64_7.dll`          | `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.1\bin` |
| `include\cudnn.h`            | `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.1\include` |
| `lib\x64\cudnn.lib`          | `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.1\lib\x64` |

---

### 6. Install OpenCV 4.9

Download **OpenCV 4.9** from the [OpenCV Releases](https://opencv.org/releases/) page.  
Run the `.exe` and extract the files to `C:\opencv`.

Add the following system environment variable:

| **System Variable** | **Value**             |
|----------------------|-----------------------|
| `OpenCV_DIR`         | `C:\opencv\build`    |

Copy the following files to `build\darknet\x64`:

| **File**                           | **Source Directory**                      |
|------------------------------------|-------------------------------------------|
| `opencv_world490d.dll`             | `C:\opencv\build\x64\vc16\bin`            |
| `opencv_world490.dll`              | `C:\opencv\build\x64\vc16\bin`            |
| `opencv_videoio_ffmpeg490_64.dll`  | `C:\opencv\build\x64\vc16\bin`            |

---

### 7. Add cuDNN DLL to Darknet

Copy `cudnn64_7.dll` to `build\darknet\x64`.

---

### 8. Download Required Files

1. **YOLOv4 Weights**:  
   Download `yolov4.conv.137` from [YOLOv4 Weights](https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.conv.137) and place it in `build\darknet\x64`.

2. **Cityscapes2Foggy Dataset**:  
   Download `Cityscaples2Foggy.zip` from [Google Drive](https://drive.google.com/file/d/1NqXY9iXXQOCPvbYpS9l8Yk66-nGzlMwQ/view?usp=sharing) and extract it to `build\darknet\x64\data`.

---

## Usage

Navigate to the `x64` directory:

```cmd
cd Project_dir\darknet\build\darknet\x64
```

### Training MS-DAYOLO

To start training, run:

```cmd
darknet detector train data/c2f.data cfg/ms-dayolo.cfg yolov4.conv.137 -dont_show -map -da
```

### Evaluation

After training, evaluate the model with:

```cmd
darknet detector map data/c2f.data cfg/ms-dayolo.cfg backup/ms-dayolo_best.weights
```

---

## Additional Information

For further details, refer to the original repository:
[GitHub - Mazin-Hnewa/MS-DAYOLO](https://github.com/Mazin-Hnewa/MS-DAYOLO)

> Compiling can be more tedious, but following these steps with the compiled one will save you much trouble as long as you set the same environment to mine

---
