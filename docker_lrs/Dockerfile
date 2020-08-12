FROM rocker/rstudio:3.5.2

WORKDIR /build

ENV DEBIAN_FRONTEND=noninteractive


RUN apt-get update \
 && apt-get install -y zlib1g-dev \
 && cd /build \
 && mkdir fftw3 \
 && cd fftw3 \
 && wget http://www.fftw.org/fftw-3.3.8.tar.gz \
 && tar -xzvf fftw-3.3.8.tar.gz \
 && cd fftw-3.3.8 \
 && ./configure --prefix=/build/fftw3 --enable-shared \
 && make && make install

RUN cd /build \
 && git clone https://remnrem@bitbucket.org/remnrem/luna-base.git \
 && git clone https://remnrem@bitbucket.org/remnrem/luna.git \
 && cd luna-base \
 && make FFTW=/build/fftw3 -j 2 \
 && ln -s /build/luna-base/luna /usr/local/bin/luna \
 && ln -s /build/luna-base/destrat /usr/local/bin/destrat \
 && ln -s /build/luna-base/behead /usr/local/bin/behead \
 && cd /build \
 && R CMD build luna \
 && LUNA_BASE=/build/luna-base FFTW=/build/fftw3 R CMD INSTALL luna_0.24.tar.gz \
 && mkdir /home/rstudio/data \
 && mkdir /home/rstudio/data1 \
 && mkdir /home/rstudio/data2 \
 && mkdir /home/rstudio/tutorial \
 && cd /home/rstudio/tutorial \
 && wget http://zzz.bwh.harvard.edu/dist/luna/tutorial.zip \
 && unzip tutorial.zip \
 && rm tutorial.zip \
 && chown -R rstudio /home/rstudio
