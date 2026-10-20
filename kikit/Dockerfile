
FROM debian:forky-slim

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        kicad \
        pipx \
        opendoas \
        python3 \
        ripgrep \
        tmux \
        unzip \
        vim \
        zsh \
        starship \
        && \
    rm -rf /var/lib/apt/lists/*

RUN pipx install --global --system-site-packages kikit

# Patch SWIG bug
RUN f=$(python3 -c "import pcbnew; print(pcbnew.__file__)") && \
    sed -i 's/\bit\.next()/next(it)/g' "$f" && \
    ! grep -q '\bit\.next()' "$f"

RUN useradd -mN -s /bin/zsh paulc

COPY doas.conf /etc/doas.conf

USER paulc
WORKDIR /home/paulc

COPY --chown=paulc:users zshrc .zshrc
COPY --chown=paulc:users vimrc .vimrc
COPY --chown=paulc:users starship.toml .config/starship.toml



