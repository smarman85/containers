FROM ubuntu:bionic

ENV GO_VERSION 1.12.6
ENV USERNAME smarman

RUN apt-get update && \
    apt-get install -y git \
      vim \
      zsh \
      wget \
      sudo \
      tmux \
      locales && \
    locale-gen "en_US.UTF-8" && \
    LC_ALL=en_US.UTF-8 && \
    LANG=en_US.UTF-8 && \
    adduser --quiet --disabled-password --shell /bin/zsh --home /home/${USERNAME} --gecos "User" ${USERNAME} && \
    wget https://dl.google.com/go/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -xvf go${GO_VERSION}.linux-amd64.tar.gz && mv go /usr/local && \
    echo "smarman ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

USER ${USERNAME}

COPY . /home/${USERNAME}

RUN git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim && \
    mkdir -p ~/.vim/colors && \
    mv /home/${USERNAME}/mustang.vim ~/.vim/colors/mustang.vim && \
    #cd /home/${USERNAME} && git clone https://github.com/powerline/fonts.git --depth=1 && \
    #./fonts/install.sh && \
    sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" && \
    cat /home/${USERNAME}/.zshrc.pre-oh-my-zsh > /home/${USERNAME}/.zshrc && \
    sed -i 's/%~/%2~/g' /home/${USERNAME}/.oh-my-zsh/themes/agnoster.zsh-theme && \
    mkdir -p /home/${USERNAME}/go/bin && mkdir -p /home/${USERNAME}/go/src

CMD ["/bin/zsh"]
