# Badic dev image 

FROM debian:trixie-slim

ENV DEBIAN_FRONTEND=noninteractive \
    RUSTUP_HOME=/usr/local/rustup \
    CARGO_HOME=/usr/local/cargo \
    PATH=/usr/local/cargo/bin:$PATH

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        zsh \
        vim \
        build-essential \
        iputils-ping \
        git \
        fzf \
        ripgrep \
        opendoas \
        ca-certificates \
        gcc-riscv64-linux-gnu && \
    rm -rf /var/lib/apt/lists/*

RUN useradd -u 501 -g 20 -mN -s /bin/zsh paulc

RUN curl -sS https://starship.rs/install.sh | sh -s -- --yes

COPY doas.conf /etc/doas.conf

USER paulc
WORKDIR /home/paulc

COPY --chown=501:20 zshrc .zshrc
COPY --chown=501:20 vimrc .vimrc
COPY --chown=501:20 starship.toml .config/starship.toml

ENV CARGO_HOME="/home/paulc/.cargo" \
    RUSTUP_HOME="/home/paulc/.rustup" \
    PATH="/home/paulc/.cargo/bin:$PATH" \
    TERM="xterm-256color"

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | \
       sh -s -- -y --default-toolchain stable --profile default
RUN rustup component add rust-analyzer 

RUN git clone --depth=1 https://github.com/rust-lang/rust.vim ~/.vim/pack/plugins/start/rust.vim
RUN git clone --depth=1 https://github.com/dense-analysis/ale.git ~/.vim/pack/plugins/start/ale


