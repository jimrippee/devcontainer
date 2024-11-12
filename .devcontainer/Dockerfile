FROM debian:unstable-slim

ARG TERRAFORM_VERSION=1.9.8
ARG PACKER_VERSION=1.11.2
ARG PWSH_VERSION=7.4.6
ARG vscode
ARG AZ_DIST=bookworm

#install some basic stuff
RUN  apt-get update && \
apt-get install -y --no-install-recommends \
iputils-ping \
iproute2 \
curl \
wget \
git \
unzip \
zsh \
python3 \
libicu-dev \
build-essential \
apt-transport-https \ 
ca-certificates \ 
gnupg \
lsb-release && \
mkdir -p /etc/apt/keyrings && \
rm -rf /var/lib/apt/lists/* && \
curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor -o /etc/apt/keyrings/microsoft.gpg

RUN echo "Types: deb\n\
URIs: https://packages.microsoft.com/repos/azure-cli/\n\
Suites: ${AZ_DIST}\n\
Components: main\n\
Architectures: $(dpkg --print-architecture)\n\
Signed-By: /etc/apt/keyrings/microsoft.gpg" \
> /etc/apt/sources.list.d/azure-cli.sources

RUN apt-get update && \
apt-get install -y --no-install-recommends azure-cli && \
rm -rf /var/lib/apt/lists/*

RUN chsh -s /bin/zsh root

RUN wget --progress=dot:mega https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip -o terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    mv terraform /usr/local/bin/ && \
    chmod +x /usr/local/bin/terraform && \
    terraform --version && \ 
    rm terraform_${TERRAFORM_VERSION}_linux_amd64.zip
    

RUN wget --progress=dot:mega https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip && \
    unzip -o packer_${PACKER_VERSION}_linux_amd64.zip && \
    mv packer /usr/local/bin/ && \
    chmod +x /usr/local/bin/packer && \
    packer --version && \
    rm packer_${PACKER_VERSION}_linux_amd64.zip

RUN wget --progress=dot:mega https://github.com/PowerShell/PowerShell/releases/download/v${PWSH_VERSION}/powershell_${PWSH_VERSION}-1.deb_amd64.deb && \
    dpkg -i powershell_${PWSH_VERSION}-1.deb_amd64.deb && \
    pwsh --version && \
    rm powershell_${PWSH_VERSION}-1.deb_amd64.deb










