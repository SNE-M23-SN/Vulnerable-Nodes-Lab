FROM kalilinux/kali-rolling

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm-256color

# Install Kali Headless and enable SSH
RUN rm -fR /var/lib/apt/ && \
    apt-get clean && \
    apt-get update -y && \
    apt-get install -y software-properties-common openssh-server --fix-missing && \
    if [ ! -d "/var/run/sshd" ]; then \
        mkdir /var/run/sshd; \
    fi && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config && \
    sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config && \
    echo 'root:kali' | chpasswd

# Update DB and clean'up!
RUN apt-get autoremove -y && \
    apt-get clean

CMD ["/usr/sbin/sshd", "-D"]
