Instalando OpenCV com NVIDIA CUDA e cuDNN:

    https://www.youtube.com/watch?v=mNgC9s1Rj60&t=12s&ab_channel=AiNSTEiNSbr


    Required programs and libraries:

    $ sudo apt install build-essential cmake git pkg-config libgtk-3-dev  libavcodec-dev libavformat-dev libswscale-dev libv4l-dev  libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev  gfortran openexr libatlas-base-dev python3-dev python3-numpy  libtbb2 libtbb-dev libdc1394-22-dev libopenexr-dev  libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev
    
    sudo apt install build-essential cmake git pkg-config libgtk-3-dev  libavcodec-dev libavformat-dev libswscale-dev libv4l-dev  libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev  gfortran openexr libatlas-base-dev python3-dev python3-numpy  libtbb2 libtbb-dev libdc1394-22-dev libopenexr-dev  libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev

    $ sudo apt install gcc-8 g++-8 gcc-9 g++-9 gcc-10 g++-10

    Creating home folder:

    $ mkdir opencv_build
    $ cd /opencv_build

    Downloading OpenCV directories:

    $ git clone https://github.com/opencv/opencv.git
    $ git clone https://github.com/opencv/opencv_contrib.git

    $ cd opencvo
    $ mkdir build
    $ cd build


    ## Check GPU architecture

    https://en.wikipedia.org/wiki/CUDA

    Change line: -D CUDA_ARCH_BIN=8.6 \ according to the architecture of the RTX 3060 Ti GPU: 8.6

    ## Verificar path do python

    $ which python3

    Change line: -D PYTHON_EXECUTABLE=/usr/bin/python3 \

    Parameterize CMake for OpenCv:

    $ cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_C_COMPILER=/usr/bin/gcc-8 \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D WITH_TBB=ON \D WITH_V4L=ON \
    -D WITH_QT=OFF \
    -D WITH_OPENGL=ON \
    -D WITH_GSTREAMER=ON \
    -D OPENCV_GENERATE_PKGCONFIG=ON \
    -D OPENCV_PC_FILE_NAME=opencv.pc \
    -D OPENCV_ENABLE_NONFREE=ON \
    -D OPENCV_PYTHON3_INSTALL_PATH=$HOME/.local/lib/python3.8/site-packages \
    -D OPENCV_EXTRA_MODULES_PATH=$HOME/opencv_build/opencv_contrib/modules \
    -D PYTHON_EXECUTABLE=/usr/bin/python3 \
    -D BUItiLD_EXAMPLES=ON \
    -D WITH_CUDA=ON \
    -D WITH_CUDNN=ON \
    -D OPENCV_DNN_CUDA=ON \
    -D ENABLE_FAST_MATH=1 \
    -D CUDA_FAST_MATH=1 \
    -D CUDA_ARCH_BIN=8.6 \
    -D BUILD_opencv_cudacodec=OFF \
    -D WITH_CUBLAS=1 \
    -D CUDNN_LIBRARY=/usr/local/cuda/lib64/libcudnn.so.8.4.0 \
    -D CUDNN_INCLUDE_DIR=/usr/local/cuda/include  ..

    Check the number of processor threads to compile faster, Rizen 5600X 12:
    
    $ nproc

    Using all threads to compile:

    $ make -j12 

    Install OpenCV:

    $ sudo make install

    Recreate the symlinks:

    $ sudo ldconfig

    Testing the library:

    $ python3

        import cv2
        print(cv2.getBuildInformation())



