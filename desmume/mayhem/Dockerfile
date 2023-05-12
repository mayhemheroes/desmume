# Build Stage:
FROM --platform=linux/amd64 ubuntu:20.04 as builder

## Install build dependencies.
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ="America/New York"
RUN apt-get update && apt-get install -y make build-essential autoconf automake libglib2.0-dev libpcap0.8 libpcap-dev libsdl2-dev zlib1g

## Add Source Code
ADD src/ /src

## Build Step
WORKDIR /src/frontend/posix
RUN ./autogen.sh && ./configure && make

# Package Stage
FROM --platform=linux/amd64 ubuntu:20.04
COPY --from=builder /src/frontend/posix/cli/desmume-cli /
RUN apt-get update && apt install -y libsdl2-2.0-0 libpcap0.8 libasound2 libx11-6 libglib2.0-0
