FROM alpine:3.8

# Switch to root for the ability to perform install
USER root

ARG VERSION

# Install tools needed for your repo-server to retrieve & decrypt secrets, render manifests
# (e.g. curl, awscli, gpg, sops)
RUN apk update && \
    apk add \
    curl \
    gnupg

# Install the AVP plugin (as root so we can copy to /usr/local/bin)
ENV AVP_VERSION=$VERSION
ENV BIN=argocd-vault-plugin
RUN curl -L -o ${BIN} https://github.com/argoproj-labs/argocd-vault-plugin/releases/download/v${AVP_VERSION}/argocd-vault-plugin_${AVP_VERSION}_linux_amd64
RUN chmod +x ${BIN}
RUN mv ${BIN} /usr/local/bin

# Switch back to non-root user
USER 999