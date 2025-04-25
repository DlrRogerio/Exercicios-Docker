# Criando e Utilizando Volumes para Persistência de Dados com MySQL

Este guia demonstra como configurar um container MySQL utilizando volumes para persistir os dados do banco de dados. Este exemplo utiliza o [repositório awesome-compose](https://github.com/docker/awesome-compose/tree/master/react-express-mysql), que contém uma aplicação React + Express + MySQL.

---

## **Passo a Passo**

### **1. Clone o Repositório**

Clone o repositório `awesome-compose` e navegue para o diretório do exemplo `react-express-mysql`:

```bash
git clone https://github.com/docker/awesome-compose.git
cd awesome-compose/react-express-mysql
```

---

### **2. Edite o Arquivo `docker-compose.yml`**

Certifique-se de que o arquivo `docker-compose.yml` está configurado para usar volumes para persistência de dados no serviço MySQL. Aqui está a configuração:

```yaml
version: '3.8'

services:
  # Serviço MySQL
  mysql:
    image: mysql:8.0
    container_name: react_express_mysql_db
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: my_database
      MYSQL_USER: user
      MYSQL_PASSWORD: password
    volumes:
      - mysql_data:/var/lib/mysql
    ports:
      - "3306:3306"

  # Serviço Backend (Express)
  backend:
    build:
      context: backend
      dockerfile: Dockerfile
    container_name: react_express_mysql_backend
    environment:
      DB_HOST: mysql
      DB_PORT: 3306
      DB_USER: user
      DB_PASSWORD: password
      DB_NAME: my_database
    depends_on:
      - mysql

  # Serviço Frontend (React)
  frontend:
    build:
      context: frontend
      dockerfile: Dockerfile
    container_name: react_express_mysql_frontend
    ports:
      - "3000:3000"
    depends_on:
      - backend

volumes:
  mysql_data:
```

---

### **3. Inicie os Containers**

Execute o seguinte comando para iniciar os serviços:

```bash
docker-compose up -d
```

---

### **4. Teste a Persistência de Dados**

1. **Insira Dados no Banco:**
   - Use o backend ou um cliente MySQL para inserir dados no banco:
     ```bash
     docker exec -it react_express_mysql_db mysql -u user -ppassword my_database
     ```
   - Execute comandos SQL para inserir dados.

2. **Pare os Containers:**
   - Pare e remova os containers:
     ```bash
     docker-compose down
     ```

3. **Reinicie os Containers:**
   - Execute novamente:
     ```bash
     docker-compose up -d
     ```

4. **Verifique os Dados:**
   - Conecte-se ao container MySQL e confira se os dados inseridos anteriormente ainda estão disponíveis.

---

## **Explicação da Configuração**

### **Serviço MySQL (`mysql`)**
- **Imagem:** Utiliza a imagem oficial do MySQL (`mysql:8.0`).
- **Credenciais:**
  - `MYSQL_ROOT_PASSWORD`: Define a senha do usuário root.
  - `MYSQL_DATABASE`: Cria um banco de dados inicial.
  - `MYSQL_USER` e `MYSQL_PASSWORD`: Definem as credenciais para o usuário da aplicação.
- **Volumes:**
  - Mapeamento `mysql_data:/var/lib/mysql` garante que os dados do banco sejam persistidos.

### **Serviço Backend (`backend`)**
- Conecta-se ao MySQL utilizando as credenciais configuradas.
- Depende do serviço MySQL para iniciar.

### **Serviço Frontend (`frontend`)**
- Fornece uma interface React para interagir com o backend.
- Depende do serviço backend para iniciar.

### **Volumes**
- O volume `mysql_data` armazena os dados de maneira persistente, garantindo que não sejam perdidos ao reiniciar ou remover os containers.

---

## **Benefícios do Uso de Volumes**
- **Persistência de Dados:** Garante que os dados do banco sejam preservados mesmo após reiniciar os containers.
- **Isolamento:** Os volumes são gerenciados pelo Docker, melhorando a segurança e simplificando o gerenciamento.
- **Backup Facilitado:** Os dados podem ser facilmente copiados ou sincronizados para backups.

---

## **Comandos Úteis**

- **Verificar Containers Ativos:**
  ```bash
  docker ps
  ```

- **Parar e Remover Containers:**
  ```bash
  docker-compose down
  ```

- **Reiniciar Serviços:**
  ```bash
  docker-compose up -d
  ```

---

Sinta-se à vontade para contribuir ou abrir uma issue no [repositório awesome-compose](https://github.com/docker/awesome-compose) se tiver dúvidas ou sugestões! 🚀
