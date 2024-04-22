# OpenCV4-CppBuilder

## Introduction
Repository offering a tutorial for installing OpenCV 4.7.0 from source in C++, including integration with CUDA and the opencv_contrib module.

## Update and Install Packages
```bash
sudo apt update
sudo apt upgrade
sudo apt-get install python3-pip
sudo apt-get install build-essential pkg-config libgtk2.0-dev libavcodec-dev libavformat-dev libjpeg-dev libswscale-dev libtiff5-dev libtbb-dev
sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
sudo apt-get install libva-dev
sudo apt-get install liblapack-dev libblas-dev
sudo apt-get install libeigen3-dev
sudo apt install cmake-gui
```

## Additional Packages Installation
```bash
pip3 install onnx
pip3 install openvino
```
## Update Again
```bash
sudo apt update
sudo apt upgrade
```

## Download and Extract OpenCV Source Code
Choose the directory and unzip the OpenCV source code: ex: Documents/
```bash
cd Documents/
wget https://github.com/opencv/opencv/archive/refs/tags/4.7.0.zip -O opencv-4.7.0.zip
wget https://github.com/opencv/opencv_contrib/archive/refs/tags/4.7.0.zip -O opencv_contrib-4.7.0.zip
unzip opencv-4.7.0.zip
unzip opencv_contrib-4.7.0.zip

mv opencv-4.7.0 opencv470
mv opencv_contrib-4.7.0 opencv_contrib
mv opencv_contrib opencv470/
```

## Configure and Build OpenCV
Check your GPU model for the appropriate ```CUDA_ARCH_BIN``` number and CPU threads for ```make -j16```:
https://developer.nvidia.com/cuda-gpus#collapseOne
```bash
mkdir build && cd build 
cmake -D CMAKE_BUILD_TYPE=RELEASE \
      -D CMAKE_INSTALL_PREFIX=/usr/local/ \
      -D OPENCV_EXTRA_MODULES_PATH=../opencv_contrib/modules \
      -D CUDA_ARCH_BIN='7.5' \
      -D WITH_CUDA=1 \
      -D WITH_V4L=ON \
      -D WITH_QT=ON \
      -D WITH_OPENGL=ON \
      -D CUDA_FAST_MATH=1 \
      -D WITH_CUBLAS=1 \
      -D OPENCV_GENERATE_PKGCONFIG=1 \
      -D ENABLE_FAST_MATH=1 \
      -D OPENCV_ENABLE_NONFREE=1 \
      -D WITH_ONNX=1 \
      -D WITH_TBB=1 \
      -D OPENCV_DNN_CUDA=1 \
      -D OPENCV_DNN_OPENVINO=1 \
      -D WITH_GTK_2_X=ON ..

sudo make -j16
sudo make install
```

## Verify Configuration
Use ```cmake-gui``` to check for any missing selections.

## Verify Installation
```bash
pkg-config --modversion opencv4
```


# Reference
https://docs.opencv.org/4.7.0/d7/d9f/tutorial_linux_install.html
https://learningsky.io/install-opencv-on-nvidia-jetson-agx-xavier/
https://developer.nvidia.com/cuda-gpus#collapseOne