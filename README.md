# Desafio Técnico 02 - 104 Programador DevOps / FUNPEC

## Proposta
Utilizando Docker Compose, produza um ou mais docker-compose.yaml que provisione a infraestrutura necessária para subir um ambiente provisionado com Postgres, Python / Django e React, em suas últimas versões, resolvendo todas as dependências necessárias. Forneça um repositório Github com o arquivo e todas as orientações necessárias para a execução do ambiente no formato Readme.md

## Sobre
Este projeto foi desenvolvido para realizar a atividade técnica 02 do processo de seleção.

## Imagens

### Configurações gerais
#### Rede
- Foi especificado um escopo de rede para o projeto rodar isoladamente.

### Web (Python / Django)
#### Considerações
- Dockerfile criado manualmente para atender as especificações do porjeto;
- O gerenciador de pacotes Pipenv foi escolhido devido a habilidade gerência de pacotes e dependências;
- Foi instalado o pacote DRF para viabilizar a comunicação entre o Django e o React;
- Foi instalado o pacote psycopg2-binary para realizar a comunicação entre o Django e o postgresql;
- O Django não suporta psycopg3, então foi instalada a última versão estável do psycopg2.
#### Pacotes do sistema
- [python3.8](https://www.python.org/)
- [pipenv](https://pipenv.pypa.io/en/latest/#install-pipenv-today)
#### Pacotes do Python
- [Django](https://www.djangoproject.com/)
- [DRF](https://www.django-rest-framework.org/)
- [psycopg2-binary](https://pypi.org/project/psycopg2-binary/)

### Postgres
#### Considerações
- Como não há especifidades relacionadas ao banco de dados, usarei a imagem do [Docker Official Images](https://docs.docker.com/docker-hub/official_images/).
- A proposta solicita o uso dos requisitos em suas últimas versões, desta forma, estou usando a tag da última versão atual.
- A tag latest não foi utilizada para que o time possa realizar a análise de impacto das atualizações da imagem.
#### Imagem
[Postgres 13.1](https://hub.docker.com/layers/postgres/library/postgres/13.1/images/sha256-38d4c14c7f71211fcf4ddd5efb3537edcdd761141ae121d5be5c64f4894276f0?context=explore)

### React
#### Considerações
- Como não tenho experiência com React, estou utilizando a estratégia definida pelo [Indrek Lasn](https://medium.com/better-programming/heres-how-you-can-use-docker-with-create-react-app-3ee3a972b04e)

## Executando o projeto

Instalar dependências python:
```
# Requisitos (ocional)
# requisitos: python 3.8
sudo apt update
sudo apt install python3-pip
sudo pip3 install pipenv
pipenv install
```
Criar projeto Djando:
```
pipenv run django-admin startproject exemplo
```
- Configurar o Database do Django no settings.py
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'example',
        'USER': 'example',
        'PASSWORD': 'example',
        'HOST': 'db',
        'POST': '5432',
    }
}
```
- Inserir o 'rest_framework' no INSTALLED_APPS do setings do django
```
INSTALLED_APPS = [
    '...',
    'rest_framework',
]
```
- configurar as informações do banco nas variáveis do Docker Compose
```
environment:
    - POSTGRES_DB=example
    - POSTGRES_USER=example
    - POSTGRES_PASSWORD=example
```

Criar o projeto react
```
sudo install npm
sudo npm install -g npx
npx create-react-app example-react
```
Criar as imagens Docker
```
docker-compose build
```
Rodar o projeto
```
docer-compose up
```
