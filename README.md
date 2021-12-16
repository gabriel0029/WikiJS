# Preparação do ambiente

### Instalação Docker
```
curl -fsSL https://get.docker.com/ | sh
```
Obs: Instalará a versão mais recente.

### Instalação o Kind
```
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.1/kind-linux-amd64
chmod +x ./kind
mv ./kind /usr/local/bin/kind
```
### Instalação o Kubectl
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

## Caso use o docker compose
### instalação 
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
## Kind

### Configuração inicial

### iniciando o kind

## Docker-compose

### Execudando o container

#docker-compose pull    # Faz o downloada das imagens.

#docker-compose up -d   # Inicia em modo demond (2º plano).

### Verificando os containers

#docker container ls                       # Lista os containers em execução.

#docker container logs -f ID_Container     # Traz os logs do serviço em execução.

#docker container inspect ID_Container     # Traz um detalhamento do container.

#docker container stats                    # Traz o status dos containers.

### finalizando container

#docker-compose stop     # Finaliza (desliga), os containers.

#docker-compose down     # Finaliza e apaga tudo relacionado as containrs.
 



### Primeiro acesso
Acesse em seu navegador http://ip_de_seu_servidor. Será carregado a página para a criação da conta de administrador, preencha os dados exigidos e clique e install para proceguir.
![Captura de tela de 2021-12-16 09-46-53](https://user-images.githubusercontent.com/87427032/146380846-5c95805a-09dd-4058-884c-d1ffa09a26d8.png)

### Criando a primeira página.
Faça o logon na página 

![Captura de tela de 2021-12-16 09-48-07](https://user-images.githubusercontent.com/87427032/146381133-71d47475-1fad-4d1c-a9a0-60a1d8613972.png)

Após o logon, será apresentado a tela de boas vindas, que também já trará a opção de criar sua primeira página.
![Captura de tela de 2021-12-16 09-48-16](https://user-images.githubusercontent.com/87427032/146381192-1b06125f-1fa6-43f1-874b-2babcf6e1d70.png)

A próxima tela é para que seja escolhido o tipo de editor. Para esse tutorial foi escolhido o tipo Markdown, mas fique a vontade e escolha o que o de sua preferência.
![Captura de tela de 2021-12-16 09-48-24](https://user-images.githubusercontent.com/87427032/146381853-be634aaa-2f26-407e-9332-f400854a8cad.png)

Coloque um título na página, descrição e dê um "OK". 
![Captura de tela de 2021-12-16 09-50-08](https://user-images.githubusercontent.com/87427032/146383258-4a1c2e68-9437-45f5-b304-08677d974cb7.png)

Obs: tem muitas possibilidade de personalização.

Agora é só adicionar o conteúdo, uma página de boas vindas, um texto simples, vai da sua imaginação. Finalizado clique em "CREATE"
![Captura de tela de 2021-12-16 09-50-59](https://user-images.githubusercontent.com/87427032/146383638-c166499d-2fb4-4efb-a34d-abaae2c2ab65.png)

Pronto, sua página foi criada e a partir desse momento você tem sua própria wiki e poderá criar os textos, tutoriais, dicas, etc.
![Captura de tela de 2021-12-16 09-51-35](https://user-images.githubusercontent.com/87427032/146383808-e4e244d3-ebf2-4aeb-8629-613bc60680b0.png)

