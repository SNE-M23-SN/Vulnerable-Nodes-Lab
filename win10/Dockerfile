FROM ubuntu:20.04

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm-256color

COPY download.py /

RUN apt-get update -y && \
    apt-get install -y \
    qemu-kvm \
    build-essential \
    libvirt-daemon-system \
    libvirt-dev \
    linux-image-5.4.0-126-generic \
    curl \
    wget \
    python3 \
    python3-pip \
    openssh-client \
    net-tools \
    jq && \
    apt-get autoremove -y && \
    apt-get clean

RUN wget https://hashicorp-releases.yandexcloud.net/vagrant/2.4.1/vagrant_2.4.1-1_amd64.deb && \
    dpkg -i vagrant_2.4.1-1_amd64.deb  && \
    rm vagrant_2.4.1-1_amd64.deb && \
    vagrant plugin install --plugin-clean-sources --plugin-source https://rubygems.org vagrant-libvirt && \
    pip3 install wldhx.yadisk-direct && \
    curl -L $(yadisk-direct https://disk.yandex.ru/d/7kDZcIIMjQZHPA) -o /tmp/windows-10-enterprise-x64-eval && \
    vagrant box add --provider libvirt --name peru/windows-10-enterprise-x64-eval /tmp/windows-10-enterprise-x64-eval && \
    vagrant init peru/windows-10-enterprise-x64-eval

COPY Vagrantfile /
COPY startup.sh /

ENTRYPOINT ["/startup.sh"]

CMD ["/bin/bash"]
