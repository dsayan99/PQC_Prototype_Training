# Multi-stage build: First the full builder image:


    FROM ubuntu:22.04

    # define the liboqs tag to be used
    ARG LIBOQS_TAG=0.11.0
    
    # liboqs build type variant; maximum portability of image:
    ARG LIBOQS_BUILD_DEFINES="-DOQS_DIST_BUILD=ON"
    
    # FROM alpine:3.20 as intermediate
    
    # Take in global args
    ARG LIBOQS_TAG
    ARG LIBOQS_BUILD_DEFINES
    
    RUN apt-get update && apt-get install -y \
        astyle\
        cmake\
        gcc\
        ninja-build\
        libssl-dev\
        python3-pytest\
        python3-pytest-xdist\
        unzip\
        xsltproc\
        doxygen\
        graphviz\
        python3-yaml\
        valgrind\
        git
    
    RUN git clone --depth 1 --branch ${LIBOQS_TAG} https://github.com/open-quantum-safe/liboqs
    
    #Build liboqs
    WORKDIR /liboqs
    RUN mkdir build && cd build && cmake -G"Ninja" ${LIBOQS_BUILD_DEFINES} -DBUILD_SHARED_LIBS=OFF .. && ninja && ninja install
    
    CMD ["bash"]