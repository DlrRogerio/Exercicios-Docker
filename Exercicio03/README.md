# Listando e Removendo Containers com Docker

Liste todos os containers em execução e parados, pare um container em execução e remova um container específico.


---

## Passos para Gerenciamento de Containers

### 1. Listar Todos os Containers
Para listar todos os containers, incluindo os que estão em execução e os que estão parados, utilize o comando:

```bash
docker ps -a
```

**Explicação:**
- `docker ps`: Lista apenas os containers em execução.
- `-a`: Exibe todos os containers, incluindo os parados.

O comando retorna uma lista com informações como o ID, nome, status e imagem de cada container.

---

### 2. Parar um Container em Execução
Para parar um container em execução, utilize o comando:

```bash
docker stop <container_id>
```

Substitua `<container_id>` pelo ID ou nome do container que deseja parar. O ID pode ser obtido na listagem de containers (`docker ps -a`).

---

### 3. Remover um Container Específico
Após parar o container, você pode removê-lo utilizando o comando:

```bash
docker rm <container_id>
```

**Nota:** Se o container ainda estiver em execução, será necessário pará-lo antes de removê-lo.

---

### Exemplo Prático
1. Liste todos os containers:
   ```bash
   docker ps -a
   ```
   Exemplo de saída:
   ```
   CONTAINER ID   IMAGE          COMMAND                  STATUS                     NAMES
   abc12345       nginx          "nginx -g 'daemon off'"   Exited (0) 10 minutes ago   meu-site
   def67890       ubuntu         "/bin/bash"              Up 5 minutes                ubuntu-container
   ```

2. Pare o container `ubuntu-container`:
   ```bash
   docker stop ubuntu-container
   ```

3. Remova o container `meu-site`:
   ```bash
   docker rm meu-site
   ```

---

## Observações Finais
- Para remover todos os containers parados, você pode usar o comando:
  ```bash
  docker container prune
  ```
  **Atenção:** Este comando removerá todos os containers parados, então use com cuidado.

Com esses comandos, você pode gerenciar seus containers de forma eficiente.
