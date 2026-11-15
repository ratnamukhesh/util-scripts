FROM ubuntu:24.04

# Prevent interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Ensure Python output is sent straight to container logs and disable .pyc files
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PIP_BREAK_SYSTEM_PACKAGES=1

# 1. Install essential system utilities and certificates required by TeamCity
RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    git \
    openssh-client \
    tar \
    unzip \
    zip \
    && rm -rf /var/lib/apt/lists/*

# 2. Install Python 3, pip, and venv (Ubuntu 24.04 includes Python 3.12)
RUN apt-get update && apt-get install -y --no-install-recommends \
    python3 \
    python3-pip \
    python3-venv \
    && ln -sf /usr/bin/python3 /usr/bin/python \
    && rm -rf /var/lib/apt/lists/*

# 3. Verify Python and pip installations
RUN python --version && pip --version

WORKDIR /workspace