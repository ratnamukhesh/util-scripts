FROM amazoncorretto:25-alpine AS builder

# Install essential CI utilities required by TeamCity and Gradle builds
RUN apk add --no-cache \
    bash \
    ca-certificates \
    curl \
    git \
    jq \
    openssh-client \
    tar \
    unzip \
    zip

# Verify Java 25 and JAVA_HOME
RUN echo "JAVA_HOME=${JAVA_HOME}" && java -version

WORKDIR /workspace