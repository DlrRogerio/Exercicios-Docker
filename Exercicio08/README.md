# Criando um Compose File para Rodar uma Aplicação com Banco de Dados

Este guia mostra como configurar um ambiente com Docker Compose contendo uma aplicação com PostgreSQL e uma interface gráfica de gerenciamento usando o pgAdmin4.

---

## **docker-compose.yml**

O arquivo abaixo configura os serviços necessários:

```yaml
version: '3.8'

services:
  # Serviço PostgreSQL
  db:
    image: postgres:15
    container_name: postgres_db
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: admin
      POSTGRES_DB: minha_aplicacao
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  # Serviço pgAdmin
  pgadmin:
    image: dpage/pgadmin4:6
    container_name: pgadmin
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@admin.com
      PGADMIN_DEFAULT_PASSWORD: admin
    ports:
      - "5050:80"
    depends_on:
      - db

volumes:
  postgres_data:
```

---

## **Passo a Passo para Uso**

### **1. Criar o Arquivo `docker-compose.yml`**
- Copie o conteúdo acima e salve no arquivo `docker-compose.yml`.

### **2. Iniciar os Serviços**
- Execute o comando:
  ```bash
  docker-compose up -d
  ```

### **3. Acessar o pgAdmin**
- Abra o navegador e acesse: [http://localhost:5050](http://localhost:5050).
- Faça login com as credenciais padrão:
  - **E-mail:** `admin@admin.com`
  - **Senha:** `admin`

### **4. Conectar ao Banco PostgreSQL no pgAdmin**
1. Após acessar o pgAdmin, clique em **"Create" → "Server"**.
2. Na aba **"General"**, insira um nome para o servidor (ex.: `PostgresLocal`).
3. Na aba **"Connection"**, preencha as informações:
   - **Host:** `db`
   - **Port:** `5432`
   - **Username:** `admin`
   - **Password:** `admin`
4. Clique em **"Save"**.

### **5. Verificar os Containers**
- Para verificar se os serviços estão rodando:
  ```bash
  docker ps
  ```

### **6. Parar os Serviços**
- Para desligar os serviços:
  ```bash
  docker-compose down
  ```

---

## **Explicação dos Componentes**

### **PostgreSQL (`db`)**
- **Imagem:** Utiliza a imagem oficial do PostgreSQL (versão 15).
- **Credenciais:** Configurado com variáveis de ambiente:
  - Usuário: `admin`
  - Senha: `admin`
  - Banco de Dados: `minha_aplicacao`
- **Porta:** Expõe a porta `5432`, padrão do PostgreSQL.
- **Volumes:** Utiliza um volume nomeado `postgres_data` para persistir os dados do banco.

### **pgAdmin (`pgadmin`)**
- **Imagem:** Utiliza a imagem oficial do pgAdmin4.
- **Credenciais:** Configuradas com variáveis de ambiente:
  - E-mail: `admin@admin.com`
  - Senha: `admin`
- **Porta:** Expõe a porta `5050` para acessar a interface gráfica.
- **depends_on:** Garante que o serviço `db` (PostgreSQL) seja iniciado antes do `pgadmin`.

---

## **Benefícios do Uso do Docker Compose**
- **Otimização do Setup:** Facilita a configuração e execução de múltiplos serviços.
- **Persistência de Dados:** O volume `postgres_data` garante que os dados do banco sejam preservados mesmo após reiniciar os containers.
- **Flexibilidade:** Fácil de escalar e ajustar os serviços conforme a necessidade.

---

Se precisar de mais ajuda ou tiver dúvidas, fique à vontade para contribuir ou abrir uma issue! 🚀
