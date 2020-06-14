FROM debian:testing-slim

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update                 \
    && apt-get -y install          \
        build-essential            \
        gcc-avr                    \
        avr-libc                   \
        binutils-avr               \
    && apt-get clean               \
    && rm -rf /var/lib/apt/lists/*