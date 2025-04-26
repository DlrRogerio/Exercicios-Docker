# Exercício 06 -  Criando e rodando um container multi-stage

Utilize um multi-stage build para otimizar uma aplicação Go, reduzindo o tamanho da imagem final. Utilize para praticar o projeto [GS PING](https://github.com/docker/docker-gs-ping)  desenvolvido em Golang.

---

## Estrutura do Dockerfile Multi-Stage

```dockerfile
# syntax=docker/dockerfile:1

# Stage 1: Build
FROM golang:1.19 AS builder

# Set destination for COPY
WORKDIR /app

# Download Go modules
COPY go.mod go.sum ./
RUN go mod download

# Copy the source code
COPY *.go ./

# Build the binary
RUN CGO_ENABLED=0 GOOS=linux go build -o /docker-gs-ping

# Stage 2: Final Image
FROM scratch

# Set working directory
WORKDIR /

# Copy the binary from the build stage
COPY --from=builder /docker-gs-ping /docker-gs-ping

# Expose the default port
EXPOSE 8080

# Command to run the binary
CMD [ "/docker-gs-ping" ]
```

### Benefícios do Multi-Stage Build

1. **Redução de Tamanho da Imagem**: A imagem final utiliza a base `scratch`, que é a menor imagem possível no Docker, contendo apenas o binário compilado.
2. **Segurança**: Remove o ambiente de desenvolvimento e dependências não necessárias, reduzindo a superfície de ataque.
3. **Performance**: Imagens menores carregam mais rápido e utilizam menos recursos.

---

## Como Construir e Rodar o Container

### 1. Clone o Repositório
Primeiramente, clone o repositório oficial do projeto GS PING:
```bash
git clone https://github.com/docker/docker-gs-ping.git
cd docker-gs-ping
```

### 2. Construa a Imagem Docker
Construa a imagem Docker utilizando o Dockerfile multi-stage:
```bash
docker build -t gs-ping-opt .
```

### 3. Execute o Container
Rode o container expondo a porta 8080:
```bash
docker run -d -p 8080:8080 gs-ping-opt
```

### 4. Teste a Aplicação
Abra o navegador e acesse:
```
http://localhost:8080
```
Ou use o `curl` para verificar a resposta:
```bash
curl http://localhost:8080
```

---

## Estrutura do Projeto

O projeto GS PING possui a seguinte estrutura:
```plaintext
.
├── Dockerfile           # Dockerfile multi-stage
├── go.mod               # Dependências do projeto
├── go.sum               # Checksum das dependências
├── main.go              # Código-fonte principal
```

---

## Comparação com o Dockerfile Original

- **Original**: Inclui o ambiente completo Golang na imagem final, resultando em um tamanho maior.
- **Multi-Stage**: Utiliza duas etapas. A primeira compila o binário e a segunda gera uma imagem final com apenas o binário, resultando em uma imagem significativamente menor e mais eficiente.

---

## Comandos Úteis

- **Verificar os Containers em Execução**:
  ```bash
  docker ps
  ```

- **Parar o Container**:
  ```bash
  docker stop <container_id>
  ```

- **Remover o Container**:
  ```bash
  docker rm <container_id>
  ```

- **Verificar os Logs do Container**:
  ```bash
  docker logs <container_id>
  ```
