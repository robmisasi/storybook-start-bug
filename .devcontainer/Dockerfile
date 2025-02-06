FROM node:22

# Install basic development tools
RUN apt update && apt install -y less man-db sudo

# Set up a non-root user (assuming `node` is the default user in the base image)
ARG USERNAME=node
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# For password-less `sudo` access, uncomment the following lines
# RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
#     && chmod 0440 /etc/sudoers.d/$USERNAME

# Set UID/GID to match host user to avoid permission issues
# Used usermod instead of useradd because assuming the user already exists
RUN usermod -u $USER_UID $USERNAME \
    && groupmod -g $USER_GID $USERNAME

RUN corepack enable
# Set `DEVCONTAINER` environment variable to help with orientation
ENV DEVCONTAINER=true