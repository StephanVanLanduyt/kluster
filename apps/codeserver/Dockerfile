FROM lscr.io/linuxserver/code-server:4.141.0@sha256:05e7025352fc8a8cdfbce07bf80c26c6dc7a0d1f1e99b2bb5e19b6a98d559897

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