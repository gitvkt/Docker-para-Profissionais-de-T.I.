# Docker-para-Profissionais-de-T.I.
# 🐳 Docker para Profissionais de T.I.

> Guia prático e progressivo para aprender Docker do zero, entender seus principais conceitos e construir ambientes profissionais utilizando containers.

![Docker](https://img.shields.io/badge/Docker-Containerization-2496ED?logo=docker\&logoColor=white)
![Docker Compose](https://img.shields.io/badge/Docker%20Compose-Orchestration-2496ED?logo=docker\&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-8.3-777BB4?logo=php\&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?logo=mysql\&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-Web%20Server-009639?logo=nginx\&logoColor=white)

---

## 📚 Sobre este projeto

Este repositório foi criado para apresentar o **Docker de forma prática e didática**, partindo dos conceitos fundamentais até a criação de um ambiente completo utilizando múltiplos containers.

O objetivo é ajudar profissionais e estudantes de T.I. a compreender:

* O que é Docker;
* O que são containers;
* O que são imagens;
* Como funciona um `Dockerfile`;
* Como utilizar volumes;
* Como funcionam as redes Docker;
* Como criar e gerenciar containers;
* Como utilizar Docker Compose;
* Como conectar diferentes serviços;
* Como criar ambientes reproduzíveis;
* Como utilizar Docker em projetos reais.

> 💡 **Não é necessário conhecimento prévio em Docker.** O conteúdo foi organizado para que uma pessoa que nunca utilizou containers consiga acompanhar o projeto.

---

# 🐳 1. O que é Docker?

Docker é uma plataforma utilizada para **criar, executar e gerenciar aplicações em containers**.

Um container fornece um ambiente isolado para executar uma aplicação juntamente com suas dependências.

Por exemplo, imagine uma aplicação PHP que precisa de:

```text
PHP 8.3
MySQL 8
Nginx
Extensões PHP
Bibliotecas
Configurações específicas
```

Sem Docker, essas ferramentas normalmente precisam ser configuradas diretamente no computador ou servidor.

Com Docker, podemos organizar esses componentes em containers:

```text
                    DOCKER
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
    ┌───────┐      ┌───────┐      ┌───────┐
    │ Nginx │      │  PHP  │      │ MySQL │
    │       │      │       │      │       │
    │Container│   │Container│    │Container│
    └───────┘      └───────┘      └───────┘
```

Cada serviço pode ser executado separadamente e os containers podem se comunicar através da rede Docker.

---

# 🤔 2. Por que utilizar Docker?

Um dos principais problemas no desenvolvimento e na administração de sistemas é a diferença entre ambientes.

Por exemplo:

```text
Desenvolvedor:
PHP 8.3
MySQL 8
Ubuntu

Servidor:
PHP 8.1
MySQL 5.7
Debian
```

Uma aplicação pode funcionar em um ambiente e apresentar problemas em outro.

Docker ajuda a padronizar esses ambientes.

```text
             MESMO AMBIENTE

Desenvolvimento ──────┐
Homologação ──────────┼──► Docker
Produção ─────────────┘
```

Entre os benefícios estão:

* Padronização;
* Isolamento;
* Reprodutibilidade;
* Facilidade de implantação;
* Facilidade para criar ambientes de desenvolvimento;
* Facilidade para testar diferentes versões;
* Automação;
* Portabilidade.

---

# 🆚 3. Docker x Máquina Virtual

Docker e máquinas virtuais não são a mesma coisa.

## Máquina Virtual

Uma máquina virtual normalmente possui seu próprio sistema operacional.

```text
COMPUTADOR
│
└── Hypervisor
    │
    ├── VM 1
    │   └── Sistema Operacional
    │
    └── VM 2
        └── Sistema Operacional
```

## Container

Containers compartilham o kernel do sistema operacional hospedeiro de uma forma diferente das VMs.

```text
COMPUTADOR
│
└── Docker
    │
    ├── Container 1
    ├── Container 2
    └── Container 3
```

Isso permite que containers sejam, em muitos cenários, mais leves e rápidos de iniciar que máquinas virtuais tradicionais.

> ⚠️ Containers não substituem máquinas virtuais em todos os cenários. Cada tecnologia possui aplicações diferentes.

---

# 🧱 4. Principais conceitos

Antes de utilizar Docker, é importante entender alguns termos.

## 📦 Imagem

Uma **imagem Docker** é um pacote imutável utilizado como base para criar containers.

Exemplos:

```text
nginx
mysql
php
ubuntu
redis
```

Podemos pensar em uma imagem como um **molde**.

```text
             IMAGEM
                │
       ┌────────┼────────┐
       ▼        ▼        ▼
 Container   Container  Container
```

---

## 📦 Container

Um **container** é uma instância executável criada a partir de uma imagem.

Exemplo:

```bash
docker run nginx
```

Esse comando utiliza a imagem do Nginx para criar e executar um container.

Uma forma simples de memorizar:

```text
IMAGE     = molde
CONTAINER = instância em execução
```

---

## 📜 Dockerfile

O `Dockerfile` contém instruções utilizadas para construir uma imagem personalizada.

Exemplo:

```dockerfile
FROM php:8.3-apache

COPY . /var/www/html

EXPOSE 80
```

Podemos construir a imagem com:

```bash
docker build -t minha-aplicacao .
```

---

## 💾 Volume

Containers são temporários por natureza.

Se um container for removido, os dados armazenados dentro dele podem ser perdidos.

Os **volumes** permitem armazenar dados fora do ciclo de vida do container.

```text
Container
    │
    ▼
Volume
    │
    ▼
Dados persistentes
```

Volumes são muito utilizados para bancos de dados.

---

## 🌐 Network

Containers podem se comunicar através das redes Docker.

Por exemplo:

```text
┌─────────────┐
│    Nginx    │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│     PHP     │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│    MySQL    │
└─────────────┘
```

---

# 💻 5. Instalação do Docker

## Windows

Para Windows, a maneira mais simples de começar é utilizando o **Docker Desktop**.

Após a instalação, abra o PowerShell ou Prompt de Comando e verifique:

```bash
docker --version
```

Exemplo:

```text
Docker version 28.x.x
```

Também podemos verificar o Docker Compose:

```bash
docker compose version
```

---

## Linux

Em distribuições Linux, o Docker pode ser instalado utilizando o gerenciador de pacotes ou os procedimentos oficiais da distribuição.

Após a instalação:

```bash
docker --version
```

E:

```bash
docker compose version
```

> 📌 Consulte sempre a documentação oficial do Docker para obter o procedimento atualizado para sua distribuição.

---

# 🚀 6. Primeiro container

Vamos executar nosso primeiro container.

```bash
docker run hello-world
```

O Docker irá:

1. Procurar a imagem `hello-world`;
2. Baixar a imagem caso ela não exista localmente;
3. Criar um container;
4. Executar o container;
5. Exibir uma mensagem de confirmação.

Para listar containers em execução:

```bash
docker ps
```

Para listar também containers parados:

```bash
docker ps -a
```

---

# 🌐 7. Executando o Nginx

Agora vamos executar um servidor web.

```bash
docker run -d -p 8080:80 --name meu-nginx nginx
```

### Entendendo o comando

```text
docker run
```

Cria e executa um container.

```text
-d
```

Executa em segundo plano.

```text
-p 8080:80
```

Mapeia:

```text
PORTA DO COMPUTADOR : PORTA DO CONTAINER
8080                 : 80
```

```text
--name meu-nginx
```

Define o nome do container.

```text
nginx
```

É a imagem utilizada.

Agora abra:

```text
http://localhost:8080
```

Você deverá visualizar a página padrão do Nginx.

---

# 📋 8. Comandos básicos

## Listar containers

```bash
docker ps
```

Todos:

```bash
docker ps -a
```

---

## Parar um container

```bash
docker stop meu-nginx
```

---

## Iniciar novamente

```bash
docker start meu-nginx
```

---

## Reiniciar

```bash
docker restart meu-nginx
```

---

## Remover

```bash
docker rm meu-nginx
```

Se estiver em execução:

```bash
docker rm -f meu-nginx
```

---

## Visualizar logs

```bash
docker logs meu-nginx
```

Acompanhar logs em tempo real:

```bash
docker logs -f meu-nginx
```

---

## Ver informações do container

```bash
docker inspect meu-nginx
```

---

# 🖼️ 9. Gerenciamento de imagens

Listar imagens:

```bash
docker images
```

Baixar uma imagem:

```bash
docker pull nginx
```

Remover uma imagem:

```bash
docker rmi nginx
```

Pesquisar imagens:

```bash
docker search nginx
```

> ⚠️ Ao utilizar imagens de terceiros, verifique sua origem, documentação, manutenção e versão.

---

# 🏗️ 10. Criando um Dockerfile

Vamos criar uma aplicação simples.

Estrutura:

```text
projeto/
│
├── Dockerfile
└── index.html
```

### index.html

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <title>Docker Demo</title>
</head>
<body>

    <h1>Olá, Docker!</h1>

    <p>Minha primeira aplicação em container.</p>

</body>
</html>
```

### Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80
```

Construir a imagem:

```bash
docker build -t minha-pagina .
```

Executar:

```bash
docker run -d -p 8080:80 --name minha-pagina minha-pagina
```

Acesse:

```text
http://localhost:8080
```

---

# 💾 11. Trabalhando com volumes

Vamos criar um volume:

```bash
docker volume create dados-mysql
```

Listar volumes:

```bash
docker volume ls
```

Inspecionar:

```bash
docker volume inspect dados-mysql
```

Volumes são especialmente importantes para bancos de dados e outros serviços que precisam manter dados entre recriações de containers.

---

# 🌐 12. Redes Docker

Criar uma rede:

```bash
docker network create minha-rede
```

Listar redes:

```bash
docker network ls
```

Executar um container conectado à rede:

```bash
docker run -d \
  --name servidor-web \
  --network minha-rede \
  nginx
```

Outro container pode ser conectado à mesma rede:

```bash
docker run -d \
  --name outro-container \
  --network minha-rede \
  nginx
```

Dentro da rede Docker, os containers podem utilizar seus nomes como nomes de host em muitos cenários.

Por exemplo:

```text
servidor-web
```

pode ser utilizado como endereço de rede para comunicação entre serviços.

---

# 🧩 13. Docker Compose

Quando um projeto possui vários containers, executar cada um manualmente pode se tornar trabalhoso.

O **Docker Compose** permite definir vários serviços em um único arquivo.

Exemplo:

```text
compose.yaml
```

```yaml
services:

  web:
    image: nginx:alpine
    ports:
      - "8080:80"

  database:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: exemplo
      MYSQL_DATABASE: sistema
```

Iniciar:

```bash
docker compose up -d
```

Visualizar:

```bash
docker compose ps
```

Ver logs:

```bash
docker compose logs
```

Parar:

```bash
docker compose down
```

---

# 🏗️ 14. Projeto Prático

Agora vamos montar um ambiente completo.

## Arquitetura

```text
                    NAVEGADOR
                        │
                        │ :8080
                        ▼
                ┌───────────────┐
                │     NGINX     │
                │   Container   │
                └───────┬───────┘
                        │
                        ▼
                ┌───────────────┐
                │      PHP      │
                │   Container   │
                └───────┬───────┘
                        │
                        ▼
                ┌───────────────┐
                │     MYSQL     │
                │   Container   │
                └───────┬───────┘
                        │
                        ▼
                    VOLUME
```

O projeto será composto por:

```text
docker-lab/
│
├── compose.yaml
│
├── nginx/
│   └── default.conf
│
├── php/
│   └── Dockerfile
│
└── src/
    └── index.php
```

---

# 📁 15. Criando o projeto

Crie a estrutura:

```text
docker-lab/
├── compose.yaml
├── nginx/
│   └── default.conf
├── php/
│   └── Dockerfile
└── src/
    └── index.php
```

---

# 🐘 16. Container PHP

Arquivo:

```text
php/Dockerfile
```

Conteúdo:

```dockerfile
FROM php:8.3-fpm

RUN docker-php-ext-install pdo pdo_mysql

WORKDIR /var/www/html
```

Esse Dockerfile utiliza PHP 8.3 com PHP-FPM e instala as extensões necessárias para comunicação com MySQL através do PDO.

---

# 🌐 17. Configurando o Nginx

Arquivo:

```text
nginx/default.conf
```

Conteúdo:

```nginx
server {
    listen 80;

    root /var/www/html;
    index index.php index.html;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include fastcgi_params;

        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;

        fastcgi_pass app:9000;
    }
}
```

Observe:

```text
fastcgi_pass app:9000;
```

`app` será o nome do serviço PHP definido no Docker Compose.

---

# 🐘 18. Criando a aplicação PHP

Arquivo:

```text
src/index.php
```

```php
<?php

echo "<h1>Docker funcionando!</h1>";

echo "<p>PHP está sendo executado dentro de um container.</p>";

echo "<p>Ambiente criado com Docker Compose.</p>";
```

---

# 🐳 19. Criando o Compose

Arquivo:

```text
compose.yaml
```

```yaml
services:

  app:
    build:
      context: ./php
    container_name: docker-php
    volumes:
      - ./src:/var/www/html
    networks:
      - docker-network

  nginx:
    image: nginx:alpine
    container_name: docker-nginx
    ports:
      - "8080:80"
    volumes:
      - ./src:/var/www/html
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
    depends_on:
      - app
    networks:
      - docker-network

  database:
    image: mysql:8.0
    container_name: docker-mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: sistema
      MYSQL_USER: usuario
      MYSQL_PASSWORD: senha
    volumes:
      - mysql-data:/var/lib/mysql
    networks:
      - docker-network

networks:
  docker-network:

volumes:
  mysql-data:
```

---

# ▶️ 20. Iniciando o ambiente

Na pasta do projeto:

```bash
docker compose up -d
```

O Docker irá:

1. Construir a imagem PHP;
2. Baixar a imagem Nginx;
3. Baixar a imagem MySQL;
4. Criar os containers;
5. Criar a rede;
6. Criar o volume;
7. Iniciar os serviços.

Verifique:

```bash
docker compose ps
```

Você deverá encontrar serviços semelhantes a:

```text
NAME           STATUS
docker-php     Running
docker-nginx   Running
docker-mysql   Running
```

---

# 🌎 21. Acessando a aplicação

Abra o navegador:

```text
http://localhost:8080
```

Você deverá visualizar:

```text
Docker funcionando!

PHP está sendo executado dentro de um container.

Ambiente criado com Docker Compose.
```

---

# 🔍 22. Verificando os logs

Para visualizar os logs:

```bash
docker compose logs
```

Somente PHP:

```bash
docker compose logs app
```

Somente Nginx:

```bash
docker compose logs nginx
```

Somente MySQL:

```bash
docker compose logs database
```

Para acompanhar em tempo real:

```bash
docker compose logs -f
```

---

# 🛑 23. Parando o ambiente

Para parar os containers:

```bash
docker compose stop
```

Para parar e remover os containers e a rede criada pelo Compose:

```bash
docker compose down
```

> Por padrão, o `docker compose down` não remove os volumes nomeados.

Para remover também os volumes:

```bash
docker compose down -v
```

> ⚠️ **ATENÇÃO:** remover o volume do MySQL apagará os dados armazenados nele.

---

# 🔐 24. Boas práticas

## Não coloque senhas reais no repositório

Evite:

```yaml
MYSQL_ROOT_PASSWORD: MinhaSenhaReal123
```

Em projetos reais, utilize variáveis de ambiente e mecanismos apropriados para gerenciamento de segredos.

---

## Utilize arquivos `.env`

Exemplo:

```text
MYSQL_ROOT_PASSWORD=senha_local
MYSQL_DATABASE=sistema
MYSQL_USER=usuario
MYSQL_PASSWORD=senha
```

E no Compose:

```yaml
environment:
  MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
  MYSQL_DATABASE: ${MYSQL_DATABASE}
  MYSQL_USER: ${MYSQL_USER}
  MYSQL_PASSWORD: ${MYSQL_PASSWORD}
```

Adicione o `.env` ao `.gitignore` quando ele contiver informações sensíveis:

```text
.env
```

---

# 🧹 25. Limpeza do ambiente

Listar containers:

```bash
docker ps -a
```

Listar imagens:

```bash
docker images
```

Listar volumes:

```bash
docker volume ls
```

Listar redes:

```bash
docker network ls
```

Para visualizar recursos que podem ser removidos:

```bash
docker system df
```

Uma limpeza mais abrangente pode ser realizada com:

```bash
docker system prune
```

> ⚠️ Leia atentamente a confirmação antes de executar comandos de limpeza. Eles podem remover recursos não utilizados.

---

# 🧪 26. Checklist de aprendizado

Ao terminar este tutorial, você deverá compreender:

* [ ] O que é Docker;
* [ ] O que é um container;
* [ ] O que é uma imagem;
* [ ] O que é um Dockerfile;
* [ ] Como criar uma imagem;
* [ ] Como executar um container;
* [ ] Como mapear portas;
* [ ] Como trabalhar com volumes;
* [ ] Como criar redes;
* [ ] Como utilizar Docker Compose;
* [ ] Como trabalhar com múltiplos containers;
* [ ] Como visualizar logs;
* [ ] Como iniciar e parar ambientes;
* [ ] Como estruturar um projeto Docker;
* [ ] Como utilizar variáveis de ambiente;
* [ ] Como preservar dados de um banco.

---

# 🧠 27. Resumo dos principais comandos

| Comando               | Função                           |
| :-------------------- | :------------------------------- |
| `docker --version`    | Verifica a versão do Docker      |
| `docker ps`           | Lista containers em execução     |
| `docker ps -a`        | Lista todos os containers        |
| `docker images`       | Lista imagens                    |
| `docker pull`         | Baixa uma imagem                 |
| `docker build`        | Constrói uma imagem              |
| `docker run`          | Cria e executa um container      |
| `docker start`        | Inicia um container              |
| `docker stop`         | Para um container                |
| `docker restart`      | Reinicia um container            |
| `docker rm`           | Remove um container              |
| `docker rmi`          | Remove uma imagem                |
| `docker logs`         | Exibe logs                       |
| `docker inspect`      | Exibe informações detalhadas     |
| `docker volume ls`    | Lista volumes                    |
| `docker network ls`   | Lista redes                      |
| `docker compose up`   | Inicia um ambiente Compose       |
| `docker compose down` | Para e remove o ambiente Compose |
| `docker compose ps`   | Lista serviços do Compose        |
| `docker compose logs` | Exibe logs dos serviços          |

---

# 📚 28. Próximos passos

Depois de dominar este laboratório, alguns temas interessantes para continuar os estudos são:

### 🔹 Docker avançado

* Multi-stage builds;
* Dockerfile otimizado;
* Healthchecks;
* Profiles;
* Build arguments;
* Docker Buildx.

### 🔹 Segurança

* Usuários não-root;
* Gerenciamento de secrets;
* Imagens mínimas;
* Atualização de dependências;
* Scanning de vulnerabilidades;
* Princípio do menor privilégio.

### 🔹 Infraestrutura

* Docker em servidores Linux;
* Reverse Proxy;
* HTTPS;
* Nginx;
* Traefik;
* Monitoramento;
* Logs centralizados.

### 🔹 DevOps

* CI/CD;
* GitHub Actions;
* Docker Registry;
* Versionamento de imagens;
* Deploy automatizado.

### 🔹 Orquestração

Depois de adquirir experiência com Docker e containers:

```text
Docker
   │
   ▼
Docker Compose
   │
   ▼
Orquestração
   │
   ▼
Kubernetes
```

---

# 🗂️ 29. Estrutura final do repositório

Uma possível organização deste projeto:

```text
docker-para-profissionais-ti/
│
├── README.md
│
├── 01-introducao/
│   └── README.md
│
├── 02-instalacao/
│   └── README.md
│
├── 03-conceitos/
│   └── README.md
│
├── 04-primeiro-container/
│   └── README.md
│
├── 05-imagens/
│   └── README.md
│
├── 06-dockerfile/
│   └── README.md
│
├── 07-volumes/
│   └── README.md
│
├── 08-redes/
│   └── README.md
│
├── 09-docker-compose/
│   └── README.md
│
├── 10-projeto-pratico/
│   ├── compose.yaml
│   ├── nginx/
│   │   └── default.conf
│   ├── php/
│   │   └── Dockerfile
│   ├── src/
│   │   └── index.php
│   └── README.md
│
├── exemplos/
│   ├── nginx/
│   ├── php/
│   ├── mysql/
│   └── wordpress/
│
└── .gitignore
```

---

# 🎯 Objetivo do laboratório

Ao finalizar este projeto, o ambiente terá:

```text
                    ┌──────────────┐
                    │   USUÁRIO    │
                    └──────┬───────┘
                           │
                           │ HTTP
                           ▼
                    ┌──────────────┐
                    │    NGINX     │
                    │   :8080      │
                    └──────┬───────┘
                           │
                           │ FastCGI
                           ▼
                    ┌──────────────┐
                    │     PHP      │
                    │    PHP-FPM   │
                    └──────┬───────┘
                           │
                           │ PDO
                           ▼
                    ┌──────────────┐
                    │    MYSQL     │
                    │     8.0      │
                    └──────┬───────┘
                           │
                           ▼
                    ┌──────────────┐
                    │    VOLUME    │
                    │  mysql-data  │
                    └──────────────┘
```

Esse laboratório demonstra uma arquitetura simples de múltiplos serviços utilizando Docker Compose e pode servir como base para projetos maiores.

---

# 📖 Referências

Para aprofundar os estudos, consulte a documentação oficial do Docker:

* [Docker Documentation](https://docs.docker.com/)
* [Docker Get Started](https://docs.docker.com/get-started/)
* [Dockerfile Reference](https://docs.docker.com/reference/dockerfile/)
* [Docker Compose Documentation](https://docs.docker.com/compose/)
* [Docker CLI Reference](https://docs.docker.com/reference/cli/docker/)

---

# 📄 Licença

Este projeto pode ser utilizado para fins de estudo, treinamento e experimentação.

Adapte o conteúdo conforme as necessidades do seu ambiente e sempre consulte a documentação oficial das ferramentas utilizadas.

---

## ⭐ Contribuição

Sugestões, correções e melhorias são bem-vindas.

Para contribuir:

```bash
git clone <URL-DO-REPOSITORIO>

cd docker-para-profissionais-ti

git checkout -b minha-melhoria
```

Faça suas alterações, registre o commit e envie um Pull Request.

---

## 👨‍💻 Autor

Projeto criado como material de estudo e referência para profissionais e estudantes de **Tecnologia da Informação, Suporte Técnico, Infraestrutura, Desenvolvimento e DevOps**.

---

<p align="center">
  🐳 <strong>Aprenda Docker. Construa ambientes. Automatize sua infraestrutura.</strong>
</p>
