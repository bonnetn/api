FROM alpine/git as cpprestsdk_sources

WORKDIR /sdk
RUN git clone https://github.com/Microsoft/cpprestsdk.git casablanca && \
      rm -rf casablanca/.git

FROM alpine as cpprestsdk_compiled
RUN apk add --update \
    boost-dev \
    cmake \
    g++ \
    libressl-dev \
    make \
    zlib-dev
WORKDIR sdk
COPY --from=cpprestsdk_sources /sdk/ ./

RUN cd casablanca/Release && \
    mkdir build.release && \
    cd build.release && \
    cmake .. -DCMAKE_BUILD_TYPE=Release && \
    make && \
    cd ./Binaries && \
    ./test_runner *_test.so

FROM alpine

RUN apk add --update \
    boost-dev \
    cmake \
    g++ \
    libressl-dev \
    make \
    zlib-dev

WORKDIR /sdk/casablanca/Release
COPY --from=cpprestsdk_compiled \
    /sdk/casablanca/Release/ \
    /sdk/casablanca/Release/
#RUN cd build.release && make install

RUN ls build.release
