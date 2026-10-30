FROM lscr.io/linuxserver/code-server:4.144.0@sha256:ec8f01d91c93a5d615224a306914c3ea9190c6237f876383591bca676a24fa67

# Define tool versions
ARG SOPS_VERSION=v3.9.4
ARG KUBESEAL_VERSION=0.40.0

# Dynamically detect architecture (amd64 / arm64) matching Debian/Ubuntu dpkg standards
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl ca-certificates tar && \
    ARCH=$(dpkg --print-architecture) && \
    \
    # 1. Download and install SOPS
    curl -Lo /usr/local/bin/sops https://github.com/getsops/sops/releases/download/${SOPS_VERSION}/sops-${SOPS_VERSION}.linux.${ARCH} && \
    chmod +x /usr/local/bin/sops && \
    \
    # 2. Download and extract Kubeseal
    curl -L https://github.com/bitnami-labs/sealed-secrets/releases/download/v${KUBESEAL_VERSION}/kubeseal-${KUBESEAL_VERSION}-linux-${ARCH}.tar.gz | tar -xz -C /usr/local/bin kubeseal && \
    chmod +x /usr/local/bin/kubeseal && \
    \
    # Clean up package lists and caches
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*