#
# export ID_RSA=$(< ~/.ssh/id_rsa_claude) ID_RSA_PUB=$(< ~/.ssh/id_rsa_claude.pub)
# container build --tag claude --secret id=ID_RSA --secret id=ID_RSA_PUB .
# 

FROM dev-base

USER root
WORKDIR /

RUN apt update && apt upgrade -y

# Copy secrets as root
RUN --mount=type=secret,id=ID_RSA cp /run/secrets/ID_RSA ~paulc/.ssh/id_rsa
RUN --mount=type=secret,id=ID_RSA_PUB cp /run/secrets/ID_RSA_PUB ~paulc/.ssh/id_rsa.pub
RUN chown -R paulc:users ~paulc/.ssh 

USER paulc
WORKDIR /home/paulc

RUN curl -fsSL https://claude.ai/install.sh > claude_install.sh


