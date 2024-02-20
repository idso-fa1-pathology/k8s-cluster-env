FROM tensorflow/tensorflow:1.13.0rc2-gpu-py3

# set environment variables
ENV DEBIAN_FRONTEND noninteractive
ENV HDF5_USE_FILE_LOCKING FALSE
ENV NUMBA_CACHE_DIR /tmp

# install libraries
RUN apt-get update && apt-get install -y --no-install-recommends \
  build-essential libgl1-mesa-glx libglib2.0-0 libgeos-dev libvips-tools libffi-dev \
  sudo curl wget htop git vim ca-certificates python3-openslide \
  && rm -rf /var/lib/apt/lists/*

# install python packages
RUN pip install pip==20.3.4
RUN pip install gpustat==0.6.0 setuptools==50.3.2 pytz==2021.1 joblib==0.14.0 tqdm==4.64.0 docopt==0.6.2
RUN pip install ipython==7.8.0 jupyterlab==3.0.0a12 notebook==6.1.6 traitlets==4.3.2 chardet==4.0.0 nbconvert==6.0.0a0
RUN pip install openslide-python==1.1.2 

WORKDIR /.local
RUN chmod -R 777 /.local
WORKDIR /.cache
RUN chmod -R 777 /.cache

# /Data folder preparation
WORKDIR /Data
RUN chmod -R 777 /Data

# bash at /App
WORKDIR /App
CMD ["/bin/bash"]