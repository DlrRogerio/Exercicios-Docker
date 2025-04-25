# Corrigindo Vulnerabilidades em Imagens Docker

Após identificar vulnerabilidades com ferramentas como o Trivy, o próximo passo é
corrigi-las. Imagens grandes e genéricas frequentemente trazem bibliotecas
desnecessárias e vulneráveis, além de usarem o usuário root por padrão. Neste
exercício, você irá trabalhar com um exemplo de Dockerfile com más práticas e
aplicar melhorias para construir uma imagem mais segura e enxuta. Identifique as
melhorias e gere uma nova versão de Dockerfile

---
 
## Dockerfile Vulnerável

Antes de realizar as correções, o `Dockerfile` original é apresentado abaixo:

````dockerfile name=Dockerfile
FROM python:3.9
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
````
---

## Problemas Identificados no Dockerfile Vulnerável

### 1. Uso de uma Imagem Base Genérica e Grande
- A imagem `python:3.9` é genérica e inclui bibliotecas e ferramentas desnecessárias, aumentando a superfície de ataque.

### 2. Uso do Usuário Root
- O container é executado como usuário root por padrão, o que é uma má prática de segurança.

### 3. Dependências Desatualizadas
- As versões de `flask` e `requests` estão desatualizadas e podem conter vulnerabilidades conhecidas.

### 4. Falta de Limpeza de Cache
- O cache de instalação de pacotes não é limpo, resultando em uma imagem maior do que o necessário.

---

## Melhorias Aplicadas no Novo Dockerfile

### Alterações Implementadas:
1. **Imagem Base Otimizada:**
   - Substituímos `python:3.9` por `python:3.9-slim`, que é uma versão enxuta da imagem base.

2. **Execução com Usuário Não Root:**
   - Criamos e utilizamos um usuário dedicado para executar a aplicação.

3. **Atualização de Dependências:**
   - Atualizamos as versões de `flask` e `requests` para corrigir possíveis vulnerabilidades.

4. **Remoção de Cache:**
   - Limpeza do cache do gerenciador de pacotes para reduzir o tamanho da imagem.

5. **Uso de Multi-stage Build (Opcional):**
   - Para imagens ainda menores, é possível usar multi-stage builds, mas aqui mantemos o foco na simplicidade.

---

## Novo Dockerfile

````dockerfile name=Dockerfile
# Usando uma imagem base reduzida
FROM python:3.9-slim

# Configurando diretório de trabalho
WORKDIR /app

# Instalando dependências do sistema necessárias
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Adicionando um usuário não root
RUN useradd -m appuser
USER appuser

# Adicionando e instalando dependências do Python
COPY --chown=appuser:appuser requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copiando o restante do código
COPY --chown=appuser:appuser . .

# Configurando o comando de inicialização
CMD ["python", "app.py"]
