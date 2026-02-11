FROM debian:12-slim

WORKDIR /app

RUN apt-get update  \
    && apt-get -y --no-install-recommends install  \
        # install any other dependencies you might need
        sudo curl git ca-certificates build-essential \
    && rm -rf /var/lib/apt/lists/*

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
ENV MISE_DATA_DIR="/mise"
ENV MISE_CONFIG_DIR="/mise"
ENV MISE_CACHE_DIR="/mise/cache"
ENV MISE_INSTALL_PATH="/usr/local/bin/mise"
ENV PATH="/mise/shims:$PATH"
# ENV MISE_VERSION="..."

RUN curl https://mise.run | sh

COPY package.json mise.toml pnpm-lock.yaml pnpm-workspace.yaml .

RUN mise install

COPY apps/api/ .

WORKDIR /app/apps/api

RUN mise run build

EXPOSE 8000

CMD ["pnpm", "preview", "--port", "3000", "--host"]
