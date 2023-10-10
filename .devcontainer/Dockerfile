FROM ubuntu:latest

# set bash as default shell
SHELL ["/bin/bash", "-c"]

# ensure coder user exists
RUN useradd -ms /bin/bash coder

# make sure there is a .bashrc file
RUN touch ~/.bashrc

# Install nvm
RUN apt update \
    && apt install -y curl \
    && apt install -y git \
    && apt install -y python3 \
    && apt install -y python3-pip \
    && apt install -y clang cmake ninja-build pkg-config libgtk-3-dev liblzma-dev \
    && apt install -y unzip 

USER coder

RUN git clone https://github.com/flutter/flutter.git ~/flutter

# clone flutter/flutter in $HOME/code/flutter
ENV PATH="/home/coder/.pub-cache/bin:/home/coder/flutter/bin:/home/coder/flutter/bin/cache/dart-sdk/bin:$PATH"
RUN flutter channel stable
RUN flutter upgrade

RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash \
    && export NVM_DIR="$HOME/.nvm" \
    && [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" \
    && [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" \
    && nvm install 18 \
    && nvm use 18 \
    && npm install -g yarn 

RUN curl -fsSL https://bun.sh/install | bash

RUN dart pub global activate fvm