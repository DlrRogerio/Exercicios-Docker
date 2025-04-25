# Criando Containers com Usuário Não Root

Este guia demonstra como criar uma imagem Docker segura, configurando-a para executar uma aplicação com um usuário não-root. Essa prática reduz os riscos de segurança ao isolar o processo de execução de privilégios elevados.

---

## **1. Dockerfile**

O exemplo abaixo mostra como configurar um `Dockerfile` para que a aplicação utilize um usuário não-root:

```dockerfile
# Use uma imagem base leve
FROM node:20-alpine

# Define o diretório de trabalho no container
WORKDIR /app

# Adiciona um usuário não-root
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Copia os arquivos do seu projeto para o container
COPY --chown=appuser:appgroup . .

# Instala as dependências do projeto
RUN npm install

# Expõe a porta que o aplicativo usará
EXPOSE 3000

# Define o usuário não-root para executar o processo
USER appuser

# Comando para iniciar a aplicação
CMD ["npm", "start"]
```

---

## **2. Explicação do Dockerfile**

- **Imagem Base (`FROM`):** Utilizamos a imagem `node:20-alpine` por ser leve e otimizada para produção.
- **Criação de Usuário (`RUN addgroup` e `adduser`):** Criamos um grupo e um usuário chamado `appuser` sem privilégios de root.
- **Permissões de Arquivos (`COPY --chown`):** Copiamos os arquivos do projeto para o container e ajustamos suas permissões para o usuário e grupo criados.
- **Definição do Usuário (`USER appuser`):** Especificamos que todos os comandos e processos subsequentes serão executados pelo usuário `appuser`.
- **CMD:** Inicia o servidor do aplicativo.

---

## **3. Construindo e Executando o Container**

1. **Construa a imagem Docker:**
   ```bash
   docker build -t minha-aplicacao-segura .
   ```

2. **Execute o container:**
   ```bash
   docker run -d -p 3000:3000 minha-aplicacao-segura
   ```

3. **Verifique se o container está rodando:**
   ```bash
   docker ps
   ```

---

## **4. Validando o Usuário no Container**

Para verificar que o container está sendo executado com o usuário não-root:

1. Acesse o container:
   ```bash
   docker exec -it <container_id> sh
   ```

2. Verifique o usuário atual:
   ```bash
   whoami
   ```
   Isso deve retornar `appuser`.

---

## **5. Benefícios de Usar Usuário Não-Root**

- **Redução de Impacto de Vulnerabilidades:** Se um invasor explorar uma vulnerabilidade, ele terá acesso limitado, pois não terá privilégios de root.
- **Boas Práticas de Segurança:** É uma prática recomendada para criar containers seguros em ambientes de produção.

---

Se precisar de mais exemplos ou ajuda com configurações específicas, fique à vontade para contribuir ou abrir uma issue! 🚀
