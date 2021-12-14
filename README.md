# Preparação do ambiente

Instalação Docker

curl -fsSL https://get.docker.com/ | sh

Instalação o Kind

curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.1/kind-linux-amd64

chmod +x ./kind

mv ./kind /usr/local/bin/kind

Instalação o Kubectl

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
