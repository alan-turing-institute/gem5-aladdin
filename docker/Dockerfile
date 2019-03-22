FROM turingboat/gem5-aladdin-boat_base as gem5-aladdin-boat
LABEL maintainer="Tomas Lazauskas"
# based on https://github.com/harvard-acc/gem5-aladdin/blob/master/docker/Dockerfile

RUN apt-get install -y scons

# cloning gem5-aladdin-boat develop branch
RUN git clone https://github.com/alan-turing-institute/gem5-aladdin-boat && \
    cd gem5-aladdin-boat && \
    git fetch && \
    git checkout develop && \
    git submodule init &&  \
    git submodule update

RUN cd /workspace/gem5-aladdin-boat && \
    scons build/X86/gem5.opt -j8

# updating the enviromental parameter
ENV ALADDIN_HOME /workspace/gem5-aladdin-boat/src/aladdin

# Install BOAT dependencies.
#   libboost-all-dev probably is an overkill but could be changed later.
RUN apt-get update; apt-get install -y \
      g++ \
      gfortran \
      gcc \
      nano

RUN apt-get update; apt-get install -y \
      libblas-dev \
      libboost-all-dev

# installing dependencies: eigen
WORKDIR "/var/tmp"
RUN git clone https://github.com/eigenteam/eigen-git-mirror
WORKDIR "/var/tmp/eigen-git-mirror"
RUN mkdir build
WORKDIR "/var/tmp/eigen-git-mirror/build"
RUN cmake ..; make; make install

#ENV PATH="/usr/local/include/eigen3:${PATH}"
ENV EIGEN_DIR="/usr/local/include/eigen3"
ENV LD_LIBRARY_PATH="/usr/local/lib:${LD_LIBRARY_PATH}"

# installing dependencies: nlopt
WORKDIR "/var/tmp"
RUN git clone git://github.com/stevengj/nlopt
WORKDIR "/var/tmp/nlopt"
RUN mkdir build
WORKDIR "/var/tmp/nlopt/build"
RUN cmake ..; make; make install

# checking out BOAT
WORKDIR "/workspace/gem5-aladdin-boat/BOAT"
RUN cd .. && \
    git submodule update --recursive --remote

# building BOAT
RUN mkdir build
WORKDIR "/workspace/gem5-aladdin-boat/BOAT/build/"
RUN ls -lrt
RUN cmake ../src; make

RUN pip install numpy
RUN pip install pyparsing==2.1.10

ENV BOAT_HOME /workspace/gem5-aladdin/BOAT

WORKDIR /workspace
