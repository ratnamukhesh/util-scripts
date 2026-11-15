
FROM ubuntu:24.04

# Prevent interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Set JAVA_HOME and update PATH
ENV JAVA_HOME=/usr/lib/jvm/java-25-amazon-corretto
ENV PATH="${JAVA_HOME}/bin:${PATH}"

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

# 2. Download and install Amazon Corretto 25 (auto-detects amd64/arm64 architecture)
RUN ARCH="$(dpkg --print-architecture)" \
    && case "${ARCH}" in \
        amd64) CORRETTO_ARCH="x64" ;; \
        arm64) CORRETTO_ARCH="aarch64" ;; \
        *) echo "Unsupported architecture: ${ARCH}" && exit 1 ;; \
    esac \
    && mkdir -p "${JAVA_HOME}" \
    && curl -fsSL "https://corretto.aws{CORRETTO_ARCH}-linux-jdk.tar.gz" -o /tmp/corretto25.tar.gz \
    && tar -xzf /tmp/corretto25.tar.gz -C "${JAVA_HOME}" --strip-components=1 \
    && rm -f /tmp/corretto25.tar.gz

# 3. Verify Java 25 and JAVA_HOME
RUN echo "JAVA_HOME=${JAVA_HOME}" && java -version

WORKDIR /workspace