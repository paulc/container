FROM dev-base-forky

USER root
WORKDIR /

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends npm && \
    rm -rf /var/lib/apt/lists/*

RUN npm install -g --allow-scripts=@anthropic-ai/claude-code @anthropic-ai/claude-code 

USER paulc
WORKDIR /home/paulc


