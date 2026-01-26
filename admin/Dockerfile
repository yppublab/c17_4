FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install -y \
    openssh-server \
    sudo \
    vim \
    postgresql-client

RUN mkdir /var/run/sshd

ARG TOLMACHEV_HASH

RUN useradd -m -s /bin/bash tolmachev && \
    echo "tolmachev:${TOLMACHEV_HASH}" | chpasswd -e && \
    usermod -aG sudo tolmachev

RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config && \
    sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin no/' /etc/ssh/sshd_config

EXPOSE 22

CMD /usr/sbin/sshd -D
