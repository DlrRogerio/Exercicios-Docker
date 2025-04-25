# Exercício 04 - Configuração de um Dockerfile para Aplicação Flask

Este guia apresenta um exemplo de configuração de um `Dockerfile` para uma aplicação Flask simples que retorna uma mensagem ao acessar um endpoint. O objetivo é criar um ambiente Docker isolado para rodar a aplicação.

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
# Usar uma imagem base do Python
FROM python:3.9-slim

# Configurar o diretório de trabalho
WORKDIR /app

# Copiar o arquivo de requisitos para o container
COPY requirements.txt requirements.txt

# Instalar as dependências do Python
RUN pip install --no-cache-dir -r requirements.txt

# Copiar os arquivos do app para o container
COPY . .

# Criar um usuário não-root
RUN adduser --disabled-password --gecos '' appuser

# Alterar a propriedade dos arquivos para o novo usuário
RUN chown -R appuser:appuser /app

# Alternar para o usuário não-root
USER appuser

# Expor a porta em que a aplicação será executada
EXPOSE 8000

# Comando para iniciar a aplicação Flask
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
