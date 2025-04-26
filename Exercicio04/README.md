# Exercício 04 - Criando um Dockerfile para uma Aplicação Simples em Python

Crie um Dockerfile para uma aplicação Flask que retorna uma mensagem ao acessar um endpoint, para isso utilize o projeto [Docker Flask](https://github.com/docker/awesome-compose/tree/master/flask).

## Preparação Inicial

1. Clone o repositório **awesome-compose** que contém o projeto base para este exercício:
   ```bash
   git clone https://github.com/docker/awesome-compose.git
   ```

2. Acesse a pasta do projeto Flask:
   ```bash
   cd awesome-compose/flask/app
   ```

3. Substitua o conteúdo do arquivo `Dockerfile` existente pelo conteúdo fornecido neste README. O arquivo `Dockerfile` já existe no projeto, mas será sobrescrito com um novo conteúdo que segue as instruções deste exercício.

Certifique-se de que o projeto tenha a seguinte estrutura de arquivos após acessar o diretório:

```
app/
├── Dockerfile
├── app.py
├── requirements.txt
```

---

## Arquivo `app.py`

Este arquivo contém o código da aplicação Flask. Ele define um endpoint que retorna uma mensagem simples:

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
	return "Hello World!"

if __name__ == '__main__':
	app.run(host='0.0.0.0', port=8000)
```

---

## Arquivo `requirements.txt`

Este arquivo lista as dependências do Python necessárias para o projeto. Certifique-se de incluir a versão correta do Flask:

```
flask
```

---

## Arquivo `Dockerfile`

O `Dockerfile` é responsável por construir a imagem Docker. Substitua o conteúdo do arquivo `Dockerfile` existente pelo seguinte:

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

### Explicação do Dockerfile
- **`FROM python:3.9-slim`**: Utiliza a imagem base do Python 3.9 otimizada para menor tamanho.
- **`WORKDIR /app`**: Define o diretório de trabalho dentro do container.
- **`COPY requirements.txt requirements.txt`**: Copia o arquivo de dependências para o container.
- **`RUN pip install --no-cache-dir -r requirements.txt`**: Instala as dependências listadas em `requirements.txt`.
- **`COPY . .`**: Copia todos os arquivos do diretório local para o container.
- **`RUN adduser --disabled-password --gecos '' appuser`**: Cria um usuário não-root chamado `appuser`.
- **`RUN chown -R appuser:appuser /app`**: Altera a propriedade dos arquivos para o usuário `appuser`.
- **`USER appuser`**: Define o usuário não-root como padrão para rodar a aplicação.
- **`EXPOSE 8000`**: Expõe a porta 8000 para o tráfego HTTP.
- **`CMD ["python", "app.py"]`**: Comando para iniciar a aplicação Flask.

---

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

---


## Conclusão

Seguindo este guia, você terá uma aplicação Flask rodando em um ambiente Docker isolado.
