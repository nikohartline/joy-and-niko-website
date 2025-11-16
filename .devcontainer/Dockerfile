FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Basic tools
RUN apt-get update && apt-get install -y \
    sudo \
    curl \
    git \
    ca-certificates \
    build-essential \
    # optional but often handy:
    pkg-config \
    libssl-dev \
    && rm -rf /var/lib/apt/lists/*

# Install uv (Python package & project manager)
# This installs uv into /root/.local/bin by default; then we symlink into /usr/local/bin
RUN curl -LsSf https://astral.sh/uv/install.sh | sh && \
    ln -s /root/.local/bin/uv /usr/local/bin/uv && \
    ln -s /root/.local/bin/uvx /usr/local/bin/uvx

# Create non-root user "vscode" with passwordless sudo (standard devcontainer pattern)
RUN useradd -m vscode && echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER vscode
WORKDIR /workspaces/app

# Optional: set a cache dir for uv (keeps things tidy & easy to mount later if you want)
ENV UV_CACHE_DIR=/home/vscode/.cache/uv