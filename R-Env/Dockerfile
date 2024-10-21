FROM hpcharbor.mdanderson.edu/jwwood/jupyter_gpu_notebook:1.0

# set environment variables
ENV DEBIAN_FRONTEND noninteractive
ENV HDF5_USE_FILE_LOCKING FALSE
ENV NUMBA_CACHE_DIR /tmp

# set web proxy
ENV http_proxy http://1mcwebproxy01.mdanderson.edu:3128
ENV https_proxy http://1mcwebproxy01.mdanderson.edu:3128
ENV HTTP_PROXY http://1mcwebproxy01.mdanderson.edu:3128
ENV HTTPS_PROXY http://1mcwebproxy01.mdanderson.edu:3128
 
RUN echo "deb http://security.ubuntu.com/ubuntu focal-security main" | sudo tee /etc/apt/sources.list.d/focal-security.list && \
    echo "deb https://cloud.r-project.org/bin/linux/ubuntu focal-cran40/">>/etc/apt/sources.list && \
    wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | sudo tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc && \
    apt-get update && \
    apt-get install -y r-base libxml2-dev locales libfontconfig1-dev libcurl4-openssl-dev libssl-dev libharfbuzz-dev libfribidi-dev libfreetype6-dev libpng-dev libtiff5-dev libjpeg-dev libopenblas-dev && \
    wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-2023.03.1-446-amd64.deb && \
    apt install -y ./rstudio-server-2023.03.1-446-amd64.deb && \
    rm -rf rstudio-server-2023.03.1-446-amd64.deb /var/lib/apt/lists/* && \
    pip install --no-cache-dir jupyter-rsession-proxy && \
    NB_GID=100 fix-permissions "${CONDA_DIR}"
RUN sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen && \
    locale-gen
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

# install packages
RUN R -e "install.packages('BiocManager', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "BiocManager::install(c('devtools', 'tidyverse'))"
RUN R -e "install.packages('stringr', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('shiny', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('tidymodels', dependencies=TRUE, repos='http://cran.rstudio.com/')"

# bash at /App
WORKDIR /App
CMD ["/bin/bash"]