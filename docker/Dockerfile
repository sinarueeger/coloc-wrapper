FROM ubuntu:16.04

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

RUN apt-get update --fix-missing && \
    apt-get install -y wget make zlib1g-dev \
    gcc gfortran bzip2 curl \
    libpcre3-dev libbz2-dev liblzma-dev libcurl4-openssl-dev g++ cmake \
    libmariadb-client-lgpl-dev libmysqlclient-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

## tabix
RUN curl -LO https://github.com/samtools/htslib/releases/download/1.9/htslib-1.9.tar.bz2 && \
    tar -xvjf htslib-1.9.tar.bz2 && cd htslib-1.9 && \
    ./configure && make && make install && cd .. && rm -rf htslib-1.9*

RUN apt-get update -y  && apt-get install -y libcairo2-dev  && apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# R 3.6
RUN wget https://cloud.r-project.org/src/base/R-3/R-3.6.1.tar.gz -P ~ && \
    tar xvzf ~/R-3.6.1.tar.gz -C ~ && \
    cd ~/R-3.6.1 && \
    ./configure --with-x=no  --enable-R-shlib=yes --with-readline=no --with-blas="-lopenblas" && \
    make && mkdir -p /usr/local/lib/R/lib && make install && cd .. && rm -rf R-3.6.1*

# R PACKAGES
ADD ./docker/install_packages.R /usr/local/bin/
RUN chmod a+x /usr/local/bin/install_packages.R && install_packages.R


## ADD R/qqplot.R /usr/local/bin/