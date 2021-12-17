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
O kind foi implementado para simular clusters Kubernetes em maquinas locais utilizando containers, com isso pode-se simular um ambiente minimo ideal de cluster kubernets (3 control-planes e 3 works).

### Configuração inicial
Crei o arquivo kind-cluster.yml, servirá para ter um padrão de criação do seu cluster. Nesse exmplo é usado apenas um contrlplane e um worker.

![Captura de tela de 2021-12-17 09-04-57](https://user-images.githubusercontent.com/87427032/146542386-23acdb1b-ff6c-4b8f-bc65-53d0d2de3a91.png)

- Iniciando o kind
```
#kind create cluster --name wikijs --config kind-cluster.yml
```
- Verificando os nós
```
#kubectl get nodes
```

### Subindo o banco e aplicações
Obtendo informações dos pods espeficico.

kubectl apply -f deployment.yml
kubectl apply -f deployment.yml
kubectl apply -f deployment.yml
kubectl apply -f deployment.yml

- Obtendo informações dos pods, deployments, services, etc.
```
#kubectl get all
```
- Obtendo informações de um pod espeficico.
```
#kubectl get pod/id_pod
```
- Obtendo informações detalhadas de um pod espeficico.
```
#kubectl describe pod/id_pod
```
### Para mais informação 

```
#kubectl --help
```


## Docker-compose
Caso use o docker compose faça o download dos arquivos, eles se encontram loga acima. aṕos isso entre no diretório para que possamos executar os containers. Ou se preferir criar os aquivos, siga os passos abaixo:

- Crie um diretório para deixar organizado e acesse ele. 
```
# mkdir docker-wikijs
# cd docker-wikijs/
```
- crie o docker-compose.yml
```
# vim docker-compose.yml

version: "3.7"
services:
  db_wikijs:
    image: postgres:14.1-alpine
    deploy:
      resources:
        limits:
          cpus: "0.3"
          memory: 500M
    volumes:
    - wikijs_data:/var/lib/postgresql/data
    env_file:
    - .env_db_wikijs
    ports:
    - "5432:5432"

  wikijs:
    image: requarks/wiki:2
    deploy:
      resources:
        limits:
          cpus: "0.2"
          memory: 300M
        reservations:
          memory: 70M
    depends_on:
    - db_wikijs
    env_file:
    - .env_wikijs
    ports:
    - "80:3000"
```
Obs: Cuidado com a identação, caso esteja mau identado, dará erro e seu container não será executado.

- Crie os arquivos de variáveis
```
# vim .env_db_wikijs 

POSTGRES_DB=wiki
POSTGRES_PASSWORD=wikijsrocks
POSTGRES_USER=wikijs
```
```
# vim .env_wikijs 

DB_TYPE=postgres
DB_HOST=db_wikijs
DB_PORT=5432
DB_USER=wikijs
DB_PASS=wikijsrocks
DB_NAME=wiki

```
- Listando os arquivos
```
#ls -lha
```
![Captura de tela de 2021-12-17 14-21-19](https://user-images.githubusercontent.com/87427032/146583545-71564ea4-8aaf-4928-a6e3-26dde2bb7fd1.png)


### Execudando o container
- Fazer o download das imagens dos containers.
```
#docker-compose pull 
```
![Captura de tela de 2021-12-17 07-52-37](https://user-images.githubusercontent.com/87427032/146535570-e6e25c72-cd0d-4a8d-bea4-469745521e77.png)
- Iniciando em modo demond (2º plano).
```
#docker-compose up -d   
```
![Captura de tela de 2021-12-17 07-53-05](https://user-images.githubusercontent.com/87427032/146535579-0caf4ddb-956c-4140-8746-2b72fcb40319.png)
### Verificando os containers
- Listand os containers em execução.
```
#docker container ls                       
```
![Captura de tela de 2021-12-17 07-53-22](https://user-images.githubusercontent.com/87427032/146535637-d6025194-3015-440d-8b71-b440e1eac43b.png)
- Visualizando os logs do serviço em execução.
```
#docker container logs -f ID_Container     #Opção -f retorna o que é acrescentado de novo ao arquivo de log da aplicação.
```
![Captura de tela de 2021-12-17 07-56-08](https://user-images.githubusercontent.com/87427032/146535723-58e1694f-81e2-4530-9440-87a9ff4530b7.png)
- Trazendo detalhamento do container.
```
#docker container inspect ID_Container
```
![Captura de tela de 2021-12-17 07-58-05](https://user-images.githubusercontent.com/87427032/146535780-08dea5a3-db15-4f80-bbd3-898e893272bc.png)
- Status dos containers.
```
#docker container stats                    
```
![Captura de tela de 2021-12-17 07-54-15](https://user-images.githubusercontent.com/87427032/146535651-37e7bb36-ee0b-4f57-9e65-936d79ee0de1.png)

### finalizando container
- Finalizando (desligando), os containers.
```
#docker-compose stop     
```
![Captura de tela de 2021-12-17 07-58-34](https://user-images.githubusercontent.com/87427032/146535925-002f1810-743c-49f7-b8e4-b428e0ded07a.png)
- Finalizando e apagando tudo relacionado aos containers.
```
#docker-compose down     
``` 
![Captura de tela de 2021-12-17 07-58-54](https://user-images.githubusercontent.com/87427032/146535946-52e8bbd2-3883-4bfa-991e-6bfb150f9130.png)



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

