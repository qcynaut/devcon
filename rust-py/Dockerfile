FROM rustlang/rust:nightly

# Install Python build dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    libncursesw5-dev \
    xz-utils \
    tk-dev \
    libxml2-dev \
    libxmlsec1-dev \
    libffi-dev \
    liblzma-dev \
    wget

# Download and install Python 3.13.2
RUN cd /tmp \
    && wget https://www.python.org/ftp/python/3.13.2/Python-3.13.2.tgz \
    && tar xzf Python-3.13.2.tgz \
    && cd Python-3.13.2 \
    && ./configure --enable-optimizations \
    && make -j$(nproc) \
    && make install \
    && cd .. \
    && rm -rf Python-3.13.2 Python-3.13.2.tgz \
    && ln -s /usr/local/bin/python3 /usr/local/bin/python \
    && ln -s /usr/local/bin/pip3 /usr/local/bin/pip

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