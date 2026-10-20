#
# export ID_RSA=$(< ~/.ssh/id_rsa_claude) ID_RSA_PUB=$(< ~/.ssh/id_rsa_claude.pub)
# container build --tag pi --secret id=ID_RSA --secret id=ID_RSA_PUB .
# 

FROM dev-base

USER root
WORKDIR /

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends npm && \
    rm -rf /var/lib/apt/lists/*

# Copy secrets as root
RUN --mount=type=secret,id=ID_RSA cp /run/secrets/ID_RSA ~paulc/.ssh/id_rsa
RUN --mount=type=secret,id=ID_RSA_PUB cp /run/secrets/ID_RSA_PUB ~paulc/.ssh/id_rsa.pub
RUN chown -R paulc:users ~paulc/.ssh 

USER paulc
WORKDIR /home/paulc

RUN curl -fsSL https://pi.dev/install.sh > pi_install.sh


