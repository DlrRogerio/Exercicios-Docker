# Construção de Rede Docker para Comunicação entre Containers (Node.js + MongoDB)

Este guia demonstra como criar redes Docker personalizadas para permitir a comunicação entre containers Node.js (backend) e MongoDB. Além disso, o frontend também será configurado para acessar o backend corretamente.

---

## **Alterações no Arquivo `docker-compose.yml`**

O arquivo `docker-compose.yml` foi modificado para incluir redes personalizadas e manter a estrutura geral do projeto inalterada. Aqui está o exemplo atualizado:

```yaml
version: '3.8'

services:
  # Serviço Backend (Node.js)
  backend:
    build:
      context: backend
      dockerfile: Dockerfile
    container_name: backend_service
    environment:
      MONGO_HOST: mongodb
      MONGO_PORT: 27017
    ports:
      - "5000:5000"
    networks:
      - backend_network

  # Serviço MongoDB
  mongodb:
    image: mongo:6
    container_name: mongodb_service
    ports:
      - "27017:27017"
    networks:
      - backend_network

  # Serviço Frontend
  frontend:
    build:
      context: frontend
      dockerfile: Dockerfile
    container_name: frontend_service
    ports:
      - "3000:3000"
    depends_on:
      - backend
    networks:
      - frontend_network
      - backend_network

networks:
  backend_network:
    driver: bridge
  frontend_network:
    driver: bridge
```

---

## **Passo a Passo**

### **1. Configurar e Iniciar os Containers**

1. **Inicie os containers usando o `docker-compose.yml`:**
   ```bash
   docker-compose up -d
   ```

2. **Verifique se os containers estão em execução:**
   ```bash
   docker ps
   ```

---

### **2. Testar a Comunicação entre os Containers**

#### **Testar Comunicação Backend ↔ MongoDB**
1. Acesse o container do backend:
   ```bash
   docker exec -it backend_service sh
   ```

2. Teste a conexão com o MongoDB:
   ```bash
   nc -zv mongodb 27017
   ```

   **Resultado esperado:**
   ```
   mongodb (172.18.0.2:27017) open
   ```

#### **Testar Comunicação Frontend ↔ Backend**
1. Abra o navegador e acesse o frontend:
   ```bash
   http://localhost:3000
   ```

2. Verifique no console do navegador ou nos logs do frontend se há comunicação com o backend.

#### **Testar Comunicação Local com MongoDB**
1. Conecte-se ao MongoDB localmente usando um cliente como o `mongosh`:
   ```bash
   mongosh --host localhost --port 27017
   ```

2. Verifique se é possível acessar o banco de dados.

---

## **Explicação das Configurações**

### **Redes Personalizadas**
- **`backend_network`:** Rede que conecta o backend ao MongoDB.
- **`frontend_network`:** Rede que conecta o frontend ao backend.

### **Serviço Backend (`backend`)**
- Configurado para se comunicar com o MongoDB por meio da rede `backend_network`.
- Porta `5000` exposta para o frontend acessar.

### **Serviço MongoDB (`mongodb`)**
- Configurado para se comunicar apenas com o backend via `backend_network`.
- Porta `27017` exposta para testes locais.

### **Serviço Frontend (`frontend`)**
- Configurado para acessar o backend por meio da porta `5000`.
- Conectado a ambas as redes `frontend_network` e `backend_network`.

---

## **Benefícios da Configuração**

1. **Isolamento:** Apenas os serviços que precisam se comunicar estão conectados na mesma rede.
2. **Segurança:** Reduz a exposição de serviços desnecessários.
3. **Escalabilidade:** Fácil de adicionar novos serviços ou redes conforme necessário.

---

## **Comandos Úteis**

- **Iniciar os Containers:**
  ```bash
  docker-compose up -d
  ```
- **Parar e Remover os Containers:**
  ```bash
  docker-compose down
  ```
- **Verificar os Containers em Execução:**
  ```bash
  docker ps
  ```
- **Acessar um Container:**
  ```bash
  docker exec -it <container_name> sh
  ```

---

Sinta-se à vontade para contribuir ou abrir uma issue para dúvidas ou melhorias! 🚀
