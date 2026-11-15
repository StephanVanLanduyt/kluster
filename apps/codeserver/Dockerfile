FROM lscr.io/linuxserver/code-server:4.145.2@sha256:20ffca4512fcfc85dcd5612fb769233c1553192392d2ec417f0859135805f40c

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