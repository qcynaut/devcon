FROM rustlang/rust:nightly

# Add non-root user with sudo privileges
RUN groupadd --gid 1000 dev \
    && useradd --uid 1000 --gid 1000 -m dev \
    && apt-get update && apt-get install -y sudo \
    && echo "dev ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/dev \
    && chmod 0440 /etc/sudoers.d/dev \
    && rm -rf /var/lib/apt/lists/*

# install rustfmt and clippy
RUN rustup component add rustfmt clippy

# install fish and oh-my-fish
RUN apt-get update && apt-get install -y \
    fish \
    && rm -rf /var/lib/apt/lists/*

# make fish the default shell
RUN chsh -s /usr/bin/fish $USER

# Install oh-my-fish
RUN curl -L https://raw.githubusercontent.com/oh-my-fish/oh-my-fish/master/bin/install > install.fish && \
    fish install.fish --noninteractive && \
    rm -f install.fish

# Install johanson omf theme
RUN fish -c "omf install johanson"

# clean up directories
RUN rm -rf /devcon

WORKDIR /home/dev
USER dev