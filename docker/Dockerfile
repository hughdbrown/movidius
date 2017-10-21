# FROM ubuntu:16.04
FROM nvidia/cuda:8.0-cudnn6-devel-ubuntu16.04
MAINTAINER Hugh Brown <hughdbrown@yahoo.com>

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        wget \
        libatlas-base-dev \
        libboost-all-dev \
        libgflags-dev \
        libgoogle-glog-dev \
        libhdf5-serial-dev \
        libleveldb-dev \
        liblmdb-dev \
        libopencv-dev \
        libprotobuf-dev \
        libsnappy-dev \
        protobuf-compiler \
        python-dev \
        python-numpy \
        python-pip \
        python-setuptools \
        python-scipy && \
    rm -rf /var/lib/apt/lists/*

ENV CAFFE_ROOT=/opt/caffe
WORKDIR $CAFFE_ROOT

# FIXME: use ARG instead of ENV once DockerHub supports this
# https://github.com/docker/hub-feedback/issues/460
ENV CLONE_TAG=1.0

RUN git clone -b ${CLONE_TAG} --depth 1 https://github.com/BVLC/caffe.git . && \
    pip install --upgrade pip && \
    cd python && pip install -r requirements.txt && cd .. && \
    git clone https://github.com/NVIDIA/nccl.git && cd nccl && make -j install && cd .. && rm -rf nccl && \
    mkdir build && cd build && \
    cmake -DUSE_CUDNN=1 -DUSE_NCCL=1 .. && \
    make -j"$(nproc)"

#    cd python && for req in $(cat requirements.txt) pydot; do pip install $req; done && cd .. && \

ENV PYCAFFE_ROOT $CAFFE_ROOT/python
ENV PYTHONPATH $PYCAFFE_ROOT:$PYTHONPATH
ENV PATH $CAFFE_ROOT/build/tools:$PYCAFFE_ROOT:$PATH
RUN echo "$CAFFE_ROOT/build/lib" >> /etc/ld.so.conf.d/caffe.conf && ldconfig

WORKDIR /workspace

#####

ENV NCS_VER "NCSDK-1.09.00.04"

RUN mkdir -p /opt/movidius && \
    git clone https://github.com/movidius/ncsdk.git

RUN  cd /workspace/ncsdk && \
    make install

#    wget http://ncs-forum-uploads.s3.amazonaws.com/ncsdk/ncsdk_01_09/${NCS_VER}.tar.gz && \
#    tar xvzf ${NCS_VER}.tar.gz && \
#    cd ${NCS_VER} && \
#    ./install-ncsdk.sh && \
