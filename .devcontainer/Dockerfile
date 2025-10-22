FROM ygsea.azurecr.io/yingeli/tensorrt_llm/release:mrope

USER root
ENV DEBIAN_FRONTEND=noninteractive
RUN curl -fsSL https://deb.nodesource.com/setup_22.x -o nodesource_setup.sh | bash - \
    && apt-get update && \
    apt-get install -y --no-install-recommends \
    bash \
    ca-certificates \
    curl \
    git \
    git-lfs \
    jq \
    locales \
    nano \
    nodejs \
    npm \
    sudo \
    && rm -rf /var/lib/apt/lists/*

# Install Claude Code
RUN npm install -g @anthropic-ai/claude-code

# Qwen3-Omni support
RUN pip install transformers==4.57.1 && \
    pip install qwen-omni-utils[decord]

# Generate the desired locale (en_US.UTF-8)
RUN locale-gen en_US.UTF-8

# Make typing unicode characters in the terminal work.
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

# Remove the `ubuntu` user and add a user `coder` so that you're not developing as the `root` user
RUN userdel -r ubuntu && \
    useradd coder \
    --create-home \
    --shell=/bin/bash \
    --uid=1000 \
    --user-group && \
    echo "coder ALL=(ALL) NOPASSWD:ALL" >>/etc/sudoers.d/nopasswd

USER coder

# Set up Claude Code config
COPY .devcontainer/claude/ /home/coder/.claude/

# Set up Codex config
# COPY .devcontainer/codex/ /home/coder/.codex/