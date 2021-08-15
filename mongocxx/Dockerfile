FROM alpine

ENV MONGOC_VERSION=1.18.0

RUN apk update &&       \
    apk add g++         \
            curl        \
            cmake       \
            openssl-dev \
            perl        \
            python3     \
            git

WORKDIR /opt

# Build mongo-c-driver
RUN curl -L -O https://github.com/mongodb/mongo-c-driver/releases/download/${MONGOC_VERSION}/mongo-c-driver-${MONGOC_VERSION}.tar.gz \
  && tar xzf mongo-c-driver-${MONGOC_VERSION}.tar.gz \
  && cd mongo-c-driver-${MONGOC_VERSION} \
  && mkdir cmake-build && cd cmake-build \
  && cmake -DENABLE_AUTOMATIC_INIT_AND_CLEANUP=OFF -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/opt/vendor -DBUILD_SHARED_LIBS=OFF -DENABLE_TESTS=OFF .. \
  && cmake --build . --target install

# Build mongo cxx driver
RUN git clone https://github.com/mongodb/mongo-cxx-driver.git --branch releases/stable --depth 1 \
  && cd mongo-cxx-driver/build \
  && cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_PREFIX_PATH=/opt/vendor -DCMAKE_INSTALL_PREFIX=/opt/vendor -DBUILD_SHARED_LIBS=OFF -DCMAKE_TESTING_ENABLED=OFF .. \
  && cmake --build . --target install \
  && apk --update --no-cache del g++ curl cmake openssl-dev perl python3 git 
