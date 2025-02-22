FROM rustlang/rust:nightly

# install fish and oh-my-fish
RUN apt-get update && apt-get install -y \
    fish \
    && rm -rf /var/lib/apt/lists/*

# make fish the default shell
RUN chsh -s /usr/bin/fish $USER

# install oh-my-fish
RUN fish -c 'curl https://raw.githubusercontent.com/oh-my-fish/oh-my-fish/master/bin/install | fish'
