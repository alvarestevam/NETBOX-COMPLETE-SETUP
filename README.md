# NetBox Complete Setup

Este repositório é uma versão customizada do projeto oficial [netbox-community/netbox-docker](https://github.com/netbox-community/netbox-docker), com foco em **simplicidade, automação e experiência de uso em ambientes reais**.

## 🎯 Objetivo

Fornecer um ambiente NetBox funcional com configurações automáticas que resolvem problemas comuns na inicialização dos containers, como:

- Erros de dependência entre serviços no momento da `migrate`.
- Ausência de um superusuário inicial.
- Comportamento não determinístico na primeira execução do Docker Compose.

---

## 🚀 Como usar

### 1. Clone o repositório
```bash
git clone https://github.com/alvarestevam/netbox-complete-setup.git
cd netbox-complete-setup
```

### 2. Configure as variáveis de ambiente
Edite os arquivos dentro de `env/` para ajustar valores como usuário, senha e banco de dados.  

**Exemplo:**  
No arquivo `env/netbox.env`, localize as variáveis:
```env
DJANGO_SUPERUSER_USERNAME=admin
DJANGO_SUPERUSER_PASSWORD=admin
```
Substitua `admin` pelo seu usuário e senha desejados.

### 3. Personalize o superusuário
Para maior controle, edite o arquivo `scripts/create_superuser.py` nas linhas abaixo:
```python
username = os.getenv("DJANGO_SUPERUSER_USERNAME", "admin")  # edite aqui
password = os.getenv("DJANGO_SUPERUSER_PASSWORD", "admin")  # edite aqui
```
Troque `admin` pelo usuário e senha que você deseja definir.

### 4. Execute com Docker Compose
```bash
docker compose up -d
```

### 5. Acesse o NetBox
Abra no navegador:  
- http://localhost:8000  
- ou http://<IP_DO_HOST>:8000  

---

## ⚠️ Aviso Importante
Por boas práticas, **modifique no diretório `/env` as senhas internas** dos seguintes serviços:  
- PostgreSQL  
- Redis  
- Redis-Cache  

---

## 👨‍💻 Autor
**Alvaro Ricarty Campos Estevam**  
[github.com/alvarestevam](https://github.com/alvarestevam)
