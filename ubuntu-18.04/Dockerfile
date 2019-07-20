FROM ubuntu:bionic

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
    adduser --quiet --disabled-password --shell /bin/zsh --home /home/smarman --gecos "User" smarman

USER smarman

COPY . /home/smarman

RUN git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim && \
    mkdir -p ~/.vim/colors && \
    mv /home/smarman/mustang.vim ~/.vim/colors/mustang.vim && \
    #cd /home/smarman && git clone https://github.com/powerline/fonts.git --depth=1 && \
    #./fonts/install.sh && \
    sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" && \
    cat /home/smarman/.zshrc.pre-oh-my-zsh > /home/smarman/.zshrc

CMD ["/bin/zsh"]
