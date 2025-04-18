FROM debian:12-slim

ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=C.UTF-8
ENV GOBIN=/usr/local/go/bin

USER root
RUN apt -y update \
    && apt -y --no-install-recommends install software-properties-common gnupg2 curl sudo \
    && curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null \
    && apt -y update \
    && apt -y --no-install-recommends install \
        git \
        iputils-ping \
        jq \
        tar \
        zip \
        nano \
        unzip \
        make \
        gcc \
        g++ \
        gdb \
        python3 \
        docker-ce \
        docker-ce-cli \
        containerd.io \
        iproute2 \
        net-tools \
    && curl -OL "https://go.dev/dl/$(curl https://go.dev/dl/?mode=json | jq -r '.[0].version').linux-$(dpkg --print-architecture).tar.gz" \
    && tar xvf "$(curl https://go.dev/dl/?mode=json | jq -r '.[0].version').linux-$(dpkg --print-architecture).tar.gz" -C /usr/local \
    && chown -R root:root /usr/local/go \
    && rm -rf go*.gz \
    && /usr/local/go/bin/go install github.com/go-delve/delve/cmd/dlv@latest \
    && usermod -aG docker root \
    && echo "export PATH=\$PATH:/usr/local/go/bin" >> /etc/bash.bashrc \
    && mkdir -p /home/root/wings \
    && echo "cd /home/root/wings && make debug" >> ~/.bashrc \
    && git config --global --add safe.directory /home/root/wings

EXPOSE 8080
EXPOSE 2022
EXPOSE 2345

WORKDIR /home/root/wings
