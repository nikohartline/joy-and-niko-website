FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Basic tools
RUN apt-get update && apt-get install -y \
    sudo \
    curl \
    git \
    ca-certificates \
    build-essential \
    pkg-config \
    libssl-dev \
    bash \
    && rm -rf /var/lib/apt/lists/*

# Install uv (Python package & project manager)
# Install script puts it in /root/.local/bin; then we copy it to /usr/local/bin
RUN curl -LsSf https://astral.sh/uv/install.sh | sh && \
    install -m 0755 /root/.local/bin/uv /usr/local/bin/uv && \
    install -m 0755 /root/.local/bin/uvx /usr/local/bin/uvx

# Create non-root user "vscode" with passwordless sudo (standard devcontainer pattern)
RUN useradd -m vscode && echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER vscode

# This is where the workspace will be mounted by the devcontainer
WORKDIR /workspaces/${localWorkspaceFolderBasename}

# Optional: set a cache dir for uv (keeps things tidy)
ENV UV_CACHE_DIR=/home/vscode/.cache/uv