Bootstrap: docker
From: nvidia/cuda:8.0-cudnn6-devel-ubuntu16.04
#From: nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

# adapted from: https://github.com/marcc-hpc/anaconda-cuda

%environment

  # use bash as default shell
  SHELL=/bin/bash

  # add CUDA paths
  CPATH="/usr/local/cuda/include:$CPATH"
  PATH="/usr/local/cuda/bin:$PATH"
  LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"
  CUDA_HOME="/usr/local/cuda"

  # add Anaconda path
  PATH="/usr/local/anaconda3/bin:$PATH"

  export PATH LD_LIBRARY_PATH CPATH CUDA_HOME

%setup
  # runs on host
  # the path to the image is $SINGULARITY_ROOTFS

%post
  # post-setup script

  # load environment variables
  . /environment

  # use bash as default shell
  echo "\n #Using bash as default shell \n" >> /environment
  echo 'SHELL=/bin/bash' >> /environment

  # make environment file executable
  chmod +x /environment

  # default mount paths
  mkdir /scratch

  #Add CUDA paths
  echo "\n #Cuda paths \n" >> /environment
  echo 'export CPATH="/usr/local/cuda/include:$CPATH"' >> /environment
  echo 'export PATH="/usr/local/cuda/bin:$PATH"' >> /environment
  echo 'export LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"' >> /environment
  echo 'export CUDA_HOME="/usr/local/cuda"' >> /environment

  # updating and getting required packages
  apt-get update && apt-get -y install locales
  locale-gen en_US.UTF-8
  apt-get install -y wget git vim build-essential cmake

  # creates a build directory
  mkdir build
  cd build

  # download and install Anaconda
  CONDA_INSTALL_PATH="/usr/local/anaconda3"
  wget https://repo.continuum.io/archive/Anaconda3-5.1.0-Linux-x86_64.sh
  chmod +x Anaconda3-5.1.0-Linux-x86_64.sh
  ./Anaconda3-5.1.0-Linux-x86_64.sh -b -p $CONDA_INSTALL_PATH

  # make and install conda environment
  #conda create -n coral python=3.6
  conda install -y python=3.6
  #source activate coral

  # standard modules
  conda install -y matplotlib
  conda install -y pytest h5py hdf5 graphviz pydot # for keras

  # tensorflow
  pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.5.0-cp36-cp36m-linux_x86_64.whl

  # keras
  pip install --ignore-installed --upgrade keras

  # TODO
  # SimpleElastix

%runscript
  # executes with the singularity run command
  # delete this section to use existing docker ENTRYPOINT command

%test
  # test that script is a success
