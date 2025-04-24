# Exercício 01 - Rodando um container básico

Execute um container usando a imagem do Nginx e acesse a página padrão no navegador. Use a [landing page do TailwindCSS](https://github.com/tailwindtoolbox/Landing-Page) como site estático dentro do container.

---

## Passos para Configuração

### 1. Atualizar os Pacotes do Sistema
Antes de começar, atualize os pacotes do sistema para garantir que tudo está atualizado.

```bash
sudo apt update
sudo apt install docker.io -y
```

### 2. Criar o Diretório do Projeto
Crie um diretório para armazenar os arquivos da aplicação.

```bash
mkdir nginx-landing
cd nginx-landing
```

### 3. Clonar o Repositório
Clone o repositório que contém os arquivos necessários para o projeto.

```bash
git clone https://github.com/tailwindtoolbox/Landing-Page
```

### 4. Criar o Dockerfile
Crie um arquivo chamado `Dockerfile` e cole o seguinte conteúdo:

```dockerfile
FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
COPY . /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

**Explicação do Dockerfile:**
- `FROM nginx:alpine` - Utiliza a imagem base do Nginx com Alpine Linux (leve e otimizada).
- `RUN rm -rf /usr/share/nginx/html/*` - Remove os arquivos padrão do Nginx.
- `COPY . /usr/share/nginx/html` - Copia os arquivos do diretório atual para o diretório padrão do Nginx.
- `EXPOSE 80` - Expõe a porta 80 para o tráfego HTTP.
- `CMD ["nginx", "-g", "daemon off;"]` - Inicia o servidor Nginx.

### 5. Construir a Imagem Docker
Construa a imagem Docker utilizando o arquivo `Dockerfile`.

```bash
docker build -t nginx-landing .
```

### 6. Executar o Container
Execute o container com o comando abaixo. Ele estará acessível na porta 8080 do seu host.

```bash
docker run --name meu-site -p 8080:80 -d nginx-landing
```

### 7. Testar no Navegador
Após executar o container, você pode testar se o servidor Nginx está funcionando acessando o seguinte endereço no navegador:

```
http://localhost:8080/
```

Se tudo estiver configurado corretamente, você verá a página do seu site.

![Landing Page feita em TailwindCSS](landing-page-taiwilnd.png)

---

## Gerenciamento do Container

### Interromper o Container
Para interromper o container em execução:

```bash
docker stop meu-site
```

O container será interrompido, mas continuará existente.

### Reiniciar o Container
Para iniciar novamente o container que foi interrompido:

```bash
docker start meu-site
```

### Remover o Container
Se você quiser remover o container completamente:

```bash
docker rm meu-site
```

---

## Observações Finais
- Certifique-se de que a porta 8080 está livre no seu host antes de executar o container.
- Para verificar os containers em execução, utilize o comando `docker ps`.
- Para listar todos os containers (inclusive os interrompidos), utilize `docker ps -a`.

Agora você tem um ambiente Nginx configurado com Docker!
