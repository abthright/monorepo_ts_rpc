
# Install package manager (npm/pnpm/ruby)
# Install grep for finding environment variables
# set working directory
# ARG >> whats this??
# RUN logic to get correct environmnet varibales
# COPY package needed to install with pnpm (package.json, pnpm-lock.yaml, etc)
# install pnpm from npm if haven't
# RUN pnpm insatll
# COPY source code (src files) to run build
# RUN pnpm build

# import nginx?
# COPY nginx.config to maka vailable
# COPY built assets (dist) to nginx folder?

# EXPOSE port used?

# start the nginx



# SUMMARY

# build stage
# install package manager
# set up work directory
# set up environment variables
# copy source code
# built the source code

# runtime stage
# move source code to nginx folder // runtime environment
# expose port
# start the nginx/server process

# note : different pipeline may apply for background jobs / go service / others


FROM debian:12-slim

WORKDIR /app

RUN apt-get update \
    && apt-get -y --no-install-recommends install \
        sudo curl git ca-certificates build-essential \
    && rm -rf /var/lib/apt/lists/*

SHELL ["/bin/bash", "-0", "pipefail", "-c"]

RUN curl https://mise.run | sh

COPY package.json pnpm-lock.yaml pnpm-workspace.yaml ./
COPY apps/platform/package.json ./apps/platform

RUN mise install

COPY . .

WORKDIR /app/apps/platform

RUN mise build

EXPOSE 4321

CMD ["mise", ""]
