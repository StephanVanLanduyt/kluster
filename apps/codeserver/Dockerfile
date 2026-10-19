FROM lscr.io/linuxserver/code-server:4.141.0@sha256:0d590a1a80a36bd2559222ad6e9f69559e962cca003f6f716b62487999d575f5

# Define the SOPS version you want to use
ARG SOPS_VERSION=v3.9.4

# Install curl, download the official SOPS binary, make it executable, and clean up
# Dynamically detect architecture (amd64 / arm64) matching Debian/Ubuntu dpkg standards
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    ARCH=$(dpkg --print-architecture) && \
    curl -Lo /usr/local/bin/sops https://github.com/getsops/sops/releases/download/${SOPS_VERSION}/sops-${SOPS_VERSION}.linux.${ARCH} && \
    chmod +x /usr/local/bin/sops && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*