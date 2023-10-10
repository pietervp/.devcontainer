FROM ubuntu:latest

RUN apt-get update \
	&& apt-get install -y \
	curl \
	git \
	golang \
	sudo \
	vim \
	wget \
	&& rm -rf /var/lib/apt/lists/*

# set bash as default shell
SHELL ["/bin/bash", "-c"]

# Install nvm
RUN apt update \
    && apt install -y curl \
    && apt install -y git \
    && apt install -y python3 \
    && apt install -y python3-pip \
    && apt install -y clang cmake ninja-build pkg-config libgtk-3-dev liblzma-dev \
    && apt install -y unzip 

ARG USER=coder
RUN useradd --create-home --groups sudo --shell /bin/bash ${USER} \
	&& echo "${USER} ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/${USER} \
	&& chmod 0440 /etc/sudoers.d/${USER}
USER ${USER}

RUN git clone https://github.com/flutter/flutter.git ~/flutter

# clone flutter/flutter in $HOME/code/flutter
ENV PATH="/home/coder/.pub-cache/bin:/home/coder/flutter/bin:/home/coder/flutter/bin/cache/dart-sdk/bin:$PATH"
RUN flutter channel stable
RUN flutter upgrade

RUN touch ~/.bashrc

RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash \
    && export NVM_DIR="${HOME}/.nvm" \
    && [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" \
    && [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" \
    && nvm install 18 \
    && nvm use 18 \
    && npm install -g yarn

# Open a new shell to source the .bashrc file and install Node.js and yarn
RUN source ~/.bashrc 

RUN curl -fsSL https://bun.sh/install | bash

RUN dart pub global activate fvm