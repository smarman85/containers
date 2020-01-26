FROM centos:centos8.1.1911

RUN yum update && \
    yum install -y epel-release \
        vim \
        git \ 
        zsh \
        unzip \ 
        https://centos7.iuscommunity.org/ius-release.rpm \
        python36u \
        python36u-pip \
        python36u-devel

CMD ["/bin/bash"]
