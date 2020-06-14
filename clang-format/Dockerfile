FROM debian:testing-slim

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update                 \
    && apt-get -y install          \
        clang-format               \
    && apt-get clean               \
    && rm -rf /var/lib/apt/lists/*