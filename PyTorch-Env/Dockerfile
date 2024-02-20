FROM nvidia/cuda:12.1.0-cudnn8-devel-ubuntu20.04

# set environment variables
ENV DEBIAN_FRONTEND noninteractive
ENV HDF5_USE_FILE_LOCKING FALSE
ENV NUMBA_CACHE_DIR /tmp

# install libraries
RUN apt-get update && apt-get install -y --no-install-recommends \
  build-essential libgl1-mesa-glx libglib2.0-0 libgeos-dev libvips-tools \
  sudo curl wget htop git vim ca-certificates python3-openslide  \
  && rm -rf /var/lib/apt/lists/*

# install Miniconda
WORKDIR /App
RUN chmod 777 /App
RUN curl -LO http://repo.continuum.io/miniconda/Miniconda3-py311_23.10.0-1-Linux-x86_64.sh
RUN bash Miniconda3-py311_23.10.0-1-Linux-x86_64.sh -p /App/miniconda -b 
RUN rm Miniconda3-py311_23.10.0-1-Linux-x86_64.sh
ENV PATH=/App/miniconda/bin:$PATH

## create a conda python 3.10 environment
RUN /App/miniconda/bin/conda install conda-build \
 && /App/miniconda/bin/conda create -y --name py310 python=3.10.13 \
 && /App/miniconda/bin/conda clean -ya
ENV CONDA_DEFAULT_ENV=py310
ENV CONDA_PREFIX=/App/miniconda/envs/$CONDA_DEFAULT_ENV
ENV PATH=$CONDA_PREFIX/bin:$PATH

# install python packages
RUN pip install gpustat==0.6.0 setuptools==61.2.0 pytz==2021.1 joblib==1.2.0 tqdm==4.64.0 docopt==0.6.2
RUN pip install ipython==8.10.0 jupyterlab==3.6.1 notebook==6.4.11 traitlets==5.9.0 chardet==5.0.0 nbconvert==7.8.0
RUN pip install openslide-python==1.3.1 Pillow==10.0.0 
RUN pip install pandas==2.1.2 matplotlib==3.7.2 seaborn==0.13.0 pycm==3.5 deepdish==0.3.7 
RUN pip install opencv-python==4.8.0.74 scikit-image==0.22.0 imgaug==0.4.0 mahotas==1.4.12 
RUN pip install scikit-learn==1.3.2 xgboost==2.0.3 statsmodels==0.13.5 lifelines==0.27.8 
RUN pip install tensorflow-hub==0.13.0 tensorflow-datasets==4.9.2 tensorboard==2.14.0
RUN conda install pytorch torchvision pytorch-cuda=12.1 -c pytorch -c nvidia
RUN pip install pyg-nightly==2.4.0.dev20231209 networkx==3.2 pysal==23.7 spatialentropy==0.0.4 
RUN pip install transformers==4.36.2 pathologyfoundation==0.1.14 ultralytics==8.0.230

# configure folder permission
WORKDIR /.dgl
RUN chmod -R 777 /.dgl
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