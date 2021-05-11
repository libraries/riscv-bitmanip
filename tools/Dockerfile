FROM buildpack-deps:xenial as builder
MAINTAINER Mohanson <mohanson@outlook.com>

RUN apt-get update && apt-get install -y git autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev

WORKDIR /source
COPY ./ .

RUN mkdir -p /opt/riscv64b
RUN cd /source && bash riscv-binutils-build.sh
RUN cd /source && bash riscv-gcc-build.sh

FROM buildpack-deps:xenial
MAINTAINER Mohanson <mohanson@outlook.com>
COPY --from=builder /opt/riscv64b /opt/riscv64b
RUN apt-get update && apt-get clean
ENV RISCV /opt/riscv64b
ENV PATH "${PATH}:${RISCV}/bin"
CMD ["riscv64-unknown-linux-gnu-gcc", "--version"]
