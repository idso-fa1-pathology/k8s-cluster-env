FROM rocker/r-ver:4.2.0
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
  build-essential curl sudo git wget vim ca-certificates \
  libglib2.0-0 libgeos-dev libxml2 libxslt-dev libglpk-dev \
  libmagick++-6.q16-dev libproj-dev libudunits2-dev \
  libpq-dev gdal-bin libgdal-dev

# folder preparation
WORKDIR /Data
RUN chmod 777 /Data
WORKDIR /App
RUN chmod 777 /App

# install packages
RUN R -e "install.packages(c('BiocManager', 'XML', 'proj4'))"
RUN R -e "BiocManager::install(c('devtools', 'tidyverse'))"


# bash at /App
WORKDIR /App
CMD ["/bin/bash"]
