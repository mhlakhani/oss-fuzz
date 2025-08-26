FROM gcr.io/oss-fuzz-base/base-builder

RUN apt-get update && apt-get install -y libssl-dev pkg-config autoconf automake libtool bison flex wget make zip cmake libglib2.0-dev patchelf

#Install Boost from source
RUN wget https://archives.boost.io/release/1.87.0/source/boost_1_87_0.tar.gz && \
    tar xzf boost_1_87_0.tar.gz && \
    cd boost_1_87_0 && \
    ./bootstrap.sh --with-toolset=clang && \
    ./b2 clean && \
    ./b2 toolset=clang -j$(nproc) install && \
    cd .. && \
    rm -rf boost_1_87_0

COPY build.sh default.options $SRC/

RUN git clone --depth 1 https://github.com/apache/thrift.git

WORKDIR $SRC/thrift 