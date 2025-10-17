FROM nvcr.io/nvidia/tensorrt-llm/release:1.2.0rc0.post1

USER root
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    bash \
    ca-certificates \
    curl \
    git \
    git-lfs \
    jq \
    locales \
    nano \
    npm \
    sudo \
    && rm -rf /var/lib/apt/lists/*

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

# Install nvm
# RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
    # && export NVM_DIR="$HOME/.nvm" \
    # && [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" \
    # && nvm install --lts \
    # && npm install -g @anthropic-ai/claude-code

# Install Claude Code
RUN npm install -g @anthropic-ai/claude-code

# Set up Claude Code config
COPY .devcontainer/claude/ /home/coder/.claude/

# Set up Codex config
# COPY .devcontainer/codex/ /home/coder/.codex/