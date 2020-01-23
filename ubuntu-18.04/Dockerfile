FROM ubuntu:bionic

ENV GO_VERSION 1.13.1
ENV USERNAME smarman

RUN apt-get update && \
    apt-get install -y git \
      vim \
      zsh \
      wget \
      sudo \
      tmux \
      curl \
      groff \
      unzip \
      python3.5 \
      #python3.6 \
      python3-pip \
      python3-venv \
      ca-certificates \
      apt-transport-https \
      software-properties-common \
      locales && \
    locale-gen "en_US.UTF-8" && \
    LC_ALL=en_US.UTF-8 && \
    LANG=en_US.UTF-8 && \
    adduser --quiet --disabled-password --shell /bin/zsh --home /home/${USERNAME} --gecos "User" ${USERNAME} && \
    wget https://dl.google.com/go/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    #wget https://releases.hashicorp.com/terraform/0.11.13/terraform_0.11.13_linux_amd64.zip && \
    #unzip terraform_0.11.13_linux_amd64.zip -d /usr/local/bin/ && \
    wget https://releases.hashicorp.com/terraform/0.12.16/terraform_0.12.16_linux_amd64.zip && \
    unzip terraform_0.12.16_linux_amd64.zip -d /usr/local/bin/ && \
    echo "smarman ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Install Docker
#RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && \
#    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" && \
#    apt-cache policy docker-ce && \
#    apt install -y docker-ce && \
#    usermod -aG docker ${USERNAME} && \
#    service docker start

# Install devops stuff
RUN pip3 install awscli && \
    wget https://releases.hashicorp.com/terraform/0.11.13/ && \
    curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb" -o "session-manager-plugin.deb" && \
    sudo dpkg -i session-manager-plugin.deb && \
    sudo start amazon-ssm-agent


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
    mkdir -p /home/${USERNAME}/go/bin && mkdir -p /home/${USERNAME}/go/src && \
    echo "export LANG=en_US.UTF-8\nexport GOROOT=/usr/local/go\nexport GOPATH=$HOME/go\nexport PATH=\$GOPATH/bin:\$GOROOT/bin:$PATH" >> /home/${USERNAME}/.zshrc

CMD ["/bin/zsh"]
