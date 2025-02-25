FROM node:22-bullseye

# Add non-root user with sudo privileges
RUN useradd --uid 1001 --gid 1000 -m dev \
    && apt-get update && apt-get install -y sudo \
    && echo "dev ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/dev \
    && chmod 0440 /etc/sudoers.d/dev \
    && rm -rf /var/lib/apt/lists/*


# enable pnpm
RUN corepack enable

# install fish and oh-my-fish
RUN apt-get update && apt-get install -y \
    fish \
    && rm -rf /var/lib/apt/lists/*

# make fish the default shell
RUN chsh -s /usr/bin/fish dev

USER dev

# Install oh-my-fish
RUN cd /home/dev && \
    curl -L https://raw.githubusercontent.com/oh-my-fish/oh-my-fish/master/bin/install > install.fish && \
    fish install.fish --noninteractive && \
    rm -f install.fish

# Install johanson omf theme
RUN fish -c "omf install johanson"

# clean up directories
RUN rm -rf /devcon
WORKDIR /home/dev