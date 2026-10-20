# Basic dev image 

FROM debian:forky-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        build-essential \
        ca-certificates \
        curl \
        fzf \
        gcc-riscv64-linux-gnu \
        git \
        htop \
        iproute2 \
        iputils-ping \
        jq \
        less \
        netcat-openbsd \
        opendoas \
        openssh-client \
        procps \
        python3 \
        ripgrep \
        starship \
        tmux \
        unzip \
        vim \
        zsh \
        && \
    rm -rf /var/lib/apt/lists/*

RUN useradd -mN -s /bin/zsh paulc

COPY doas.conf /etc/doas.conf

USER paulc
WORKDIR /home/paulc

COPY --chown=paulc:users zshrc .zshrc
COPY --chown=paulc:users vimrc .vimrc
COPY --chown=paulc:users starship.toml .config/starship.toml
COPY --chown=paulc:users --chmod=755 gen_deploy_key.sh gen_deploy_key.sh 

ENV CARGO_HOME="/home/paulc/.cargo" \
    RUSTUP_HOME="/home/paulc/.rustup" \
    PATH="/home/paulc/.cargo/bin:$PATH" \
    TERM="xterm-256color"

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | \
       sh -s -- -y --default-toolchain stable --profile default
RUN rustup component add rust-analyzer 

RUN curl -LsSf https://astral.sh/uv/install.sh | sh
RUN curl -LsSf https://deno.land/install.sh | sh

RUN ssh-keygen -t rsa -b 4096 -C "paulc@" -N "" -f ~/.ssh/id_rsa
RUN git config --global init.defaultBranch main
RUN git config --global user.name "pc" && git config --global user.email "pc@"

RUN git clone --depth=1 https://github.com/rust-lang/rust.vim ~/.vim/pack/plugins/start/rust.vim
RUN git clone --depth=1 https://github.com/dense-analysis/ale.git ~/.vim/pack/plugins/start/ale

