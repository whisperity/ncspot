FROM krallin/ubuntu-tini:bionic

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -qq \
    && apt-get install -qqy --no-install-recommends \
        build-essential \
        ca-certificates \
        curl \
        libncursesw5-dev \
        libdbus-1-dev \
        libpulse-dev \
        libssl-dev \
        libxcb1-dev \
        libxcb-render0-dev \
        libxcb-shape0-dev \
        libxcb-xfixes0-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs > rust.sh \
    && chmod +x rust.sh \
    && sh rust.sh -y \
    && rm rust.sh \
    && echo "source $HOME/.cargo/env" >> $HOME/.bashrc

ENTRYPOINT ["/usr/local/bin/tini", "--", "/bin/bash", "-lc"]
CMD ["cargo install ncspot --root /mnt"]
