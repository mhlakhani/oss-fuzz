FROM gcr.io/oss-fuzz-base/base-builder-jvm

RUN apt-get update && apt-get install -y libssl-dev pkg-config autoconf automake libtool bison flex wget make ant zip curl

# Install Boost from source
RUN wget https://archives.boost.io/release/1.87.0/source/boost_1_87_0.tar.gz && \
    tar xzf boost_1_87_0.tar.gz && \
    cd boost_1_87_0 && \
    ./bootstrap.sh --with-toolset=clang && \
    ./b2 clean && \
    ./b2 toolset=clang -j$(nproc) install && \
    cd .. && \
    rm -rf boost_1_87_0

# Download and install Gradle
RUN cd /usr/local && \
    curl -L https://services.gradle.org/distributions/gradle-8.13-bin.zip -o gradle-8.13-bin.zip && \
    unzip gradle-8.13-bin.zip && \
    rm gradle-8.13-bin.zip

ENV GRADLE_HOME=/usr/local/gradle-8.13
ENV PATH=$PATH:$GRADLE_HOME/bin

COPY build.sh $SRC/

RUN git clone --depth 1 https://github.com/apache/thrift.git

WORKDIR $SRC/thrift 