FROM rocker/r-ver:4.2.0
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
  build-essential curl sudo git wget vim ca-certificates \
  libglib2.0-0 libgeos-dev libxml2 libxslt-dev libglpk-dev \
  libmagick++-6.q16-dev libproj-dev libudunits2-dev \
  libpq-dev gdal-bin libgdal-dev

# install packages
RUN R -e "install.packages('BiocManager', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "BiocManager::install(c('devtools', 'tidyverse'))"
RUN R -e "install.packages('stringr', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('shiny', dependencies=TRUE, repos='http://cran.rstudio.com/')"
RUN R -e "install.packages('tidymodels', dependencies=TRUE, repos='http://cran.rstudio.com/')"

# /Data folder preparation
WORKDIR /Data
RUN chmod -R 777 /Data

# bash at /App
WORKDIR /App
CMD ["/bin/bash"]