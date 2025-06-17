NetBox Complete Setup

Este repositório é uma versão customizada do projeto oficial netbox-community/netbox-docker, com foco em simplicidade, automação e experiência de uso em ambientes reais.

Objetivo:

Fornecer um ambiente NetBox funcional com configurações automáticas que resolvem problemas comuns da inicialização do container, como:

- Erro de dependência entre serviços no momento da migrate.

- Ausência de um superusuário inicial.

- Comportamento não determinístico na primeira execução do Docker Compose.


📂 Estrutura do Repositório

netbox-complete-setup/
├── Dockerfile
├── docker-compose.yml           
├── docker-compose.override.yml   
├── env/
│   ├── netbox.env                
│   ├── postgres.env              
│   └── redis.env               
├── configuration/               
│   ├── configuration.py
│   ├── extra.py
│   ├── logging.py
│   ├── plugins.py
│   └── ldap/
│        ├── extra.py
│        └── ldap_config.py
├── scripts/
│   └── create_superuser.py   
├── docker/
│   ├── configuration.docker.py
│   ├── docker-entrypoint.sh
│   ├── housekeeping.sh
│   ├── nginx-unit.json
│   ├── unit.list
│   ├── lauch-netbox.sh
│   └── ldap_config.docker.py
└── README.md

Como usar:

1- Clone o repositório

git clone https://github.com/alvarestevam/netbox-complete-setup.git
cd netbox-complete-setup

2- Configure as variáveis de ambiente

Edite os arquivos dentro de env/ para ajustar os valores como usuário, senha e banco:

DJANGO_SUPERUSER_USERNAME=admin                <----- edite aqui
DJANGO_SUPERUSER_PASSWORD=admin                <----- edite aqui
DJANGO_SUPERUSER_EMAIL=admin@example.com

3- Para personalizar o superusuário criado automaticamente, edite o arquivo scripts/create_superuser.py:

import os
from django.contrib.auth import get_user_model

username = os.getenv("DJANGO_SUPERUSER_USERNAME", "admin")                <----- edite aqui
password = os.getenv("DJANGO_SUPERUSER_PASSWORD", "admin")                <----- edite aqui
email = os.getenv("DJANGO_SUPERUSER_EMAIL", "admin@example.com")

User = get_user_model()

if not User.objects.filter(username=username).exists():
    print(f"Creating superuser '{username}'...")
    User.objects.create_superuser(username=username, email=email, password=password)
else:
    print(f"Superuser '{username}' already exists.")

4- Execute com Docker Compose

docker compose up -d

5- Acesse o NetBox

No navegador: http://localhost:8000 ou http://<IP DO HOST>:8000


Esse projeto é uma contribuição para a comunidade com base em experiências reais. Pull requests e feedbacks são bem-vindos!

Autor:

Alvaro Ricarty Campos Estevam
github.com/alvarestevam
