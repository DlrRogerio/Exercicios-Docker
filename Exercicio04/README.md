# Exercício 04 - Criando um Dockerfile para uma aplicação simples em Python

Crie um Dockerfile para uma aplicação Flask que retorna uma mensagem ao acessar um endpoint, para isso utilize o projeto [Docker Flask](https://github.com/docker/awesome-compose/tree/master/flask/app)

## Estrutura do Projeto

Certifique-se de que o projeto tenha a seguinte estrutura de arquivos:

```
project/
├── Dockerfile
├── app.py
├── requirements.txt
```

### Arquivo `app.py`

Este arquivo contém o código da aplicação Flask. Ele define um endpoint que retorna uma mensagem simples.

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
	return "Hello World!"

if __name__ == '__main__':
	app.run(host='0.0.0.0', port=8000)
```

### Arquivo `requirements.txt`

Este arquivo lista as dependências do Python necessárias para o projeto. Certifique-se de incluir a versão correta do Flask.

```
flask
```

### Arquivo `Dockerfile`

O `Dockerfile` é responsável por construir a imagem Docker. Ele inclui todas as etapas necessárias, como instalação de dependências, criação de usuário não-root e configuração do ambiente para rodar a aplicação Flask.

```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
RUN adduser --disabled-password --gecos '' appuser
RUN chown -R appuser:appuser /app
USER appuser
EXPOSE 8000
CMD ["python", "app.py"]
```

## Passos para Construir e Executar o Container

### 1. Construir a Imagem Docker

Navegue até o diretório do projeto e execute o seguinte comando para construir a imagem Docker:

```bash
docker build -t flask-docker-app .
```

### 2. Executar o Container

Após a construção da imagem, execute o seguinte comando para iniciar o container:

```bash
docker run -d -p 8000:8000 --name flask-app-container flask-docker-app
```

### 3. Verificar se a Aplicação Está Funcionando

Abra o navegador ou use uma ferramenta como `curl` para acessar o endpoint:

```
http://localhost:8000/
```

A resposta esperada será:

```
Hello World!
```

4. **Verificar Permissões**
   Certifique-se de que os arquivos da aplicação possuem permissões adequadas para o usuário não-root criado no `Dockerfile`.

## Conclusão

Seguindo este guia, você terá uma aplicação Flask rodando em um ambiente Docker isolado, com segurança adicional ao rodar como usuário não-root.
