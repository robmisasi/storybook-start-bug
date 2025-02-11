FROM ubuntu:noble

# Install basic development tools
RUN apt update && apt install -y bash git less man-db sudo && apt clean

# Add user "node"
ARG USERNAME=node
ARG USER_UID=2000
ARG USER_GID=$USER_UID

RUN useradd -m -s /usr/bin/bash -u $USER_UID $USERNAME \
    && groupmod -g $USER_GID $USERNAME

# Install NodeJS
ENV NODE_MAJOR="22"

RUN apt-get update \
    && apt-get install -y ca-certificates curl gnupg \
    && mkdir -p /etc/apt/keyrings \
    && curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg \
    && echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | tee /etc/apt/sources.list.d/nodesource.list \
    && apt-get update \
    && apt-get install -y nodejs \
    && apt-get clean

# Install yarn
RUN corepack enable \
    && su - $USERNAME -c "corepack install -g yarn"

ENV COREPACK_ENABLE_NETWORK=0
ENV COREPACK_ENABLE_PROJECT_SPEC=0
ENV DEVCONTAINER=true

CMD ["/usr/bin/bash", "-l"]