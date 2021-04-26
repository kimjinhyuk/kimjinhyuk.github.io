---
layout: post
title: Install Tensorflow and OpenCV on M1 Mac 
excerpt: M1 mac으로 설치 하는데 삽질을 여러번 했기 때문에 성공한 버전을 기록하기 위해 블로그에 작성해 놓음. 
categories: [Machine Learning, Deep Learning, AI, Conda]
use_math: true
comments: true
tag: [Conda,M1 mac, Macbook, Tensorflow, OpenCV]
---

# M1 Mac Install Conda environment and CV



```Python
### Install miniconda arm63 apple silicon version
$ brew install miniforge
$ brew install cmake
$ pip install --force wheel setuptools cached-property six packaging
$ pip install --upgrade --no-dependencies --force numpy-1.18.5-cp38-cp38-macosx_11_0_arm64.whl grpcio-1.33.2-cp38-cp38-macosx_11_0_arm64.whl h5py-2.10.0-cp38-cp38-macosx_11_0_arm64.whl tensorflow_addons_macos-0.1a3-cp38-cp38-macosx_11_0_arm64.whl
### 버전이 다른 파일을 받을 수 있으니 파일명을 잘 봐야 할 듯
$ pip install absl-py astunparse flatbuffers gast google_pasta keras_preprocessing opt_einsum protobuf tensorflow_estimator termcolor typing_extensions wrapt wheel tensorboard typeguard
$ pip install --upgrade --force --no-dependencies tensorflow_macos-0.1a3-cp38-cp38-macosx_11_0_arm64.whl
$ wget -O opencv-4.5.1.zip https://github.com/opencv/opencv/archive/4.5.1.zip
$ wget -O opencv_contrib-4.5.1.zip https://github.com/opencv/opencv_contrib/archive/4.5.1.zip
$ unzip opencv-4.5.1.zip
$ unzip opencv_contrib-4.5.1.zip
$ cd opencv-4.5.1
$ mkdir build && cd build
$ where python3 #경로 확인
$ cd opencv_contrib-4.5.1/modules
$ cmake \
  -DCMAKE_SYSTEM_PROCESSOR=arm64 \
  -DCMAKE_OSX_ARCHITECTURES=arm64 \
  -DWITH_OPENJPEG=OFF \
  -DWITH_IPP=OFF \
  -D CMAKE_BUILD_TYPE=RELEASE \
  -D CMAKE_INSTALL_PREFIX=/usr/local \
  -D OPENCV_EXTRA_MODULES_PATH=/Users/jin/opencv_contrib-4.5.1/modules \ #본인 경로에 맞게
  -D PYTHON3_EXECUTABLE=/Users/jin/miniforge3/envs/tf/bin/python3 \ #본인 경로에 맞게
  -D BUILD_opencv_python2=OFF \
  -D BUILD_opencv_python3=ON \
  -D INSTALL_PYTHON_EXAMPLES=ON \
  -D INSTALL_C_EXAMPLES=OFF \
  -D OPENCV_ENABLE_NONFREE=ON \
  -D BUILD_EXAMPLES=ON ..
$ make -j8
$ sudo make install
$ mdfind cv2.cpython
$ cd ~/miniforge3/envs/tf/lib/python3.8/site-packages 
$ ln -s /usr/local/lib/python3.8/site-packages/cv2/python-3.8/cv2.cpython-38-darwin.so cv2.so

# 주의 : 응용프로그램 -> 유틸리티 -> 터미널에서 오른쪽 버튼 -> 정보 가져오기 -> Rosetta를 사용하여 열기에 체크되어 있음 안됨
```

출처 : http://javaspecialist.co.kr/board/1059;jsessionid=CEFD0C00045D290CAFCAA4DC43921389