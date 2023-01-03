FROM ubuntu:18.04 AS builder

WORKDIR /build
RUN sed -i s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g /etc/apt/sources.list; \
    apt-get update -y; \
    apt install -y g++ make 

COPY Makefile /build/
COPY src /build/src
RUN mkdir -p obj ;\
    mkdir -p bin ;\
    make 

FROM ubuntu:18.04 

WORKDIR /challenge
COPY --from=builder /build/bin/hts_bus_challenge /challenge/

CMD ["/challenge/hts_bus_challenge"]
