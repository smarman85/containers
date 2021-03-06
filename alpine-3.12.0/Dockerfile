FROM alpine:3.12.0

ENV GO_VERSION 1.15.2
#ENV TF_VERSION 0.12.16
ENV TF_VERSION 0.11.14
ENV HELM_VERSION v2.16.0-rc.2
ENV K8S_VERSION v1.17.0
ENV USERNAME smarman
ENV USERID 1000

RUN apk update && \
    apk upgrade && \
    apk add --no-cache --virtual \
    vim \
    zsh \
    openssh \
    curl \
    git \
    gcc \
    python3 \
    build-base \
    linux-headers && \
    adduser --home /home/${USERNAME} --uid ${USERID} --shell /bin/zsh $USERNAME --disabled-password && \
    echo "${USERNAME} ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers 


RUN curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb" -o "session-manager-plugin.deb" && \
    #sudo dpkg -i session-manager-plugin.deb && \
    wget https://releases.hashicorp.com/terraform/${TF_VERSION}/terraform_${TF_VERSION}_linux_amd64.zip && \
    unzip terraform_${TF_VERSION}_linux_amd64.zip -d /usr/local/bin/ && \
    wget https://get.helm.sh/helm-${HELM_VERSION}-linux-amd64.tar.gz && \
    tar -zxvf helm-${HELM_VERSION}-linux-amd64.tar.gz && \
    mv linux-amd64/helm /usr/local/bin/helm && \
    curl -LO https://storage.googleapis.com/kubernetes-release/release/${K8S_VERSION}/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl

USER ${USERNAME}

COPY . /home/${USERNAME}

RUN git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim && \
    mkdir -p ~/.vim/colors && \
    mv /home/${USERNAME}/mustang.vim ~/.vim/colors/mustang.vim && \
    #cd /home/${USERNAME} && git clone https://github.com/powerline/fonts.git --depth=1 && \
    #./fonts/install.sh && \
    sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" && \
    #cat /home/${USERNAME}/.zshrc.pre-oh-my-zsh > /home/${USERNAME}/.zshrc && \
    sed -i 's/%~/%2~/g' /home/${USERNAME}/.oh-my-zsh/themes/agnoster.zsh-theme && \
    mkdir -p /home/${USERNAME}/go/bin && mkdir -p /home/${USERNAME}/go/src && \
    echo "export LANG=en_US.UTF-8\nexport GOROOT=/usr/local/go\nexport GOPATH=$HOME/go\nexport PATH=\$GOPATH/bin:\$GOROOT/bin:$PATH" >> /home/${USERNAME}/.zshrc

CMD ["/bin/sh"]
