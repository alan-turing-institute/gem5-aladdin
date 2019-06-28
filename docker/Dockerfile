FROM turingboat/gem5-aladdin-boat_base as gem5-aladdin-boat
LABEL maintainer="Tomas Lazauskas"
# based on https://github.com/harvard-acc/gem5-aladdin/blob/master/docker/Dockerfile

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

ENV BOAT_HOME="/workspace/gem5-aladdin/BOAT"

# While we are developing the packages keep the following two RUN commands
RUN cd /workspace/gem5-aladdin-boat && \
    rm -rf BOAT && \
    git clone https://github.com/alan-turing-institute/BOAT && \
    cd BOAT && \
    git fetch && \
    git checkout develop

ENV PYTHONPATH="$PYTHONPATH:/workspace/gem5-aladdin/BOAT_plus"

RUN cd /workspace/gem5-aladdin-boat && \
    rm -rf BOAT_plus && \
    git clone https://github.com/alan-turing-institute/BOAT_plus && \
    cd BOAT_plus && \
    git fetch 

WORKDIR /workspace
