In this tutorial we will learn  How to install CUDA, cuDNN, PyTorch for RTX 30xx using Ubuntu 20.04 LTS in 06/06/2022

    $ sudo apt-get --purge remove "*cublas*" "*cufft*" "*curand*" "*cusolver*" "*cusparse*" "*npp*" "*nvjpeg*" "cuda*" "nsight*"
    $ sudo apt-get --purge remove "*nvidia*"
    $ sudo apt-get autoremove
    $ sudo apt-get autoclean
    $ sudo rm -rf /usr/local/cuda*

Install latest nvidia drivers:

    Through the PPA:

    Abrir o programa software & Updates:

    1 - Other software -> Add-> APT line: ppa:graphics-drivers/ppa ->   +Add Source -> close reload cache

    2 - Additional Drivers escolher o mais recente disponivel -> Aplay changes -> reboot PC

    Via site:
 
    https://www.nvidia.com.br/Download/index.aspx?lang=br

Install CUDA Toolki 11.3.1:

    Here are commands to install:

    First step install gcc:

    $ sudo apt update
    $ sudo apt upgrade
    $ sudo apt install build-essential
    $ sudo apt-get install manpages-dev
    $ sudo apt install gcc

    Download CUDA Toolki 11.3.1:

    Reference Link:

    https://developer.nvidia.com/cuda-11-3-1-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&target_type=runfile_local

    $ wget https://developer.download.nvidia.com/compute/cuda/11.3.1/local_installers/cuda_11.3.1_465.19.01_linux.run

    $ sudo sh cuda_11.3.1_465.19.01_linux.run

    Update PATH:

    $ sudo nano .bashrc

    Add two lines at the end of the file:

    export PATH=$PATH:/usr/local/cuda/bin
    export LD_LIBRARY_PATH=/usr/local/cuda/lib64

    Reload the PATH::

    $ source .bashrc

    Check installation::

    $ nvcc -V

Install o CUDANN:

    Reference Link:

    https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html

    cuDNN Download

    download: Local Installer for Linux x86_64 (Tar)

    cudnn-linux-x86_64-8.4.1.50_cuda11.6-archive
    
    Unzip

    $ tar -xvf cudnn-linux-x86_64-8.4.1.50_cuda11.6-archive.tar.xz
    
    Enter the unzipped folder and copy the files to the respective directories:

    $ cd cudnn-linux-x86_64-8.4.1.50_cuda11.6-archive
    $ cd include 
    $ sudo  cp * /usr/local/cuda/include

    Check if files have been copied:

    $ ls /usr/local/cuda/include
    $ cd ../lib
    $ sudo  cp * /usr/local/cuda/lib64

    Check if files have been copied:

    $ ls /usr/local/cuda/lib64
    
    Update user access permissions:

    $ sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*

    cd ../include/
    
    $ sudo cp -P cudnn.h /usr/include
    $ cd ../lib/
    $ sudo cp -P libcudnn* /usr/lib/x86_64-linux-gnu/
    $ sudo chmod a+r /usr/lib/x86_64-linux-gnu/libcudnn*

    Recreate the symlinks:

    $ cd ~ 
    $ sudo ldconfig
    
    Check the installation path:

    $ whereis cudnn

    Check if the installation is correct:

    $ nvcc -V
    $ nvidia-smi
    

Install Pytorch 1.11.0 stable for yolov5:

    https://pytorch.org/get-started/locally/
    
    $ sudo apt install python3-pip

    $ sudo pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu113
    
    Additional libraries for yolov5:
    
    $ sudo pip3 install pandas
    $ sudo pip3 install tqdm
    $ sudo pip3 install matplotlib
    $ sudo pip3 install seaborn
    $ sudo apt install libopencv-dev