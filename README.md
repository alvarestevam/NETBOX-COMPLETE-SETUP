NetBox Complete Setup

Este repositório é uma versão customizada do projeto oficial netbox-community/netbox-docker, com foco em simplicidade, automação e experiência de uso em ambientes reais.

Objetivo:

Fornecer um ambiente NetBox funcional com configurações automáticas que resolvem problemas comuns da inicialização do container, como:

- Erro de dependência entre serviços no momento da migrate.

- Ausência de um superusuário inicial.

- Comportamento não determinístico na primeira execução do Docker Compose.

Como usar:

1- Clone o repositório

"git clone https://github.com/alvarestevam/netbox-complete-setup.git" e em seguida
"cd netbox-complete-setup"

2- Configure as variáveis de ambiente

Edite os arquivos dentro de env/ para ajustar os valores como usuário, senha e banco:

Exemplo
Modificar usuario padrão:
Dentro do env/netbox.env terá duas variaveis que são "DJANGO_SUPERUSER_USERNAME=admin" e "DJANGO_SUPERUSER_PASSWORD=admin", Apenas modifique as informções para seu usuario nos campos "admin".

3- Para personalizar o superusuário criado automaticamente, edite o arquivo scripts/create_superuser.py:

Seguintes linhas que precisam ser modificadas:
"username = os.getenv("DJANGO_SUPERUSER_USERNAME", "admin")"  <----- edite aqui / "password = os.getenv("DJANGO_SUPERUSER_PASSWORD", "admin")"  <----- edite aqui

Necessario apenas substituir os campos "admin" por seu usuario e senha.

4- Execute com Docker Compose

docker compose up -d

5- Acesse o NetBox

No navegador: http://localhost:8000 ou http://<IP DO HOST>:8000


Esse projeto é uma contribuição para a comunidade com base em experiências reais. Pull requests e feedbacks são bem-vindos!

Autor:

Alvaro Ricarty Campos Estevam
github.com/alvarestevam
