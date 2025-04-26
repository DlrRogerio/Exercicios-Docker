# Exercicios-Docker

Este repositório contém a resolução completa de uma lista de exercícios Docker, divididos em níveis de dificuldade: **Fácil**, **Médio** e **Difícil**. Cada exercício tem seus comandos explicados, capturas de tela (se necessário), e instruções de execução.

---

## ✅ Pré-requisitos

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Git](https://git-scm.com/)
- [Trivy](https://github.com/aquasecurity/trivy) (para o exercício 11)
- Navegador para visualizar páginas web

---

## 🟢 Fácil

### 1. [Rodando um container básico (Nginx + TailwindCSS)](Exercicio01/README.md)  
- Executa um container com Nginx.
- Usa uma landing page do TailwindCSS como conteúdo estático.

### 2. [Container interativo com Ubuntu](Exercicio02/README.md)  
- Acessa o terminal bash.
- Roda scripts e instala pacotes manualmente.

### 3. [Listando e removendo containers](Exercicio03/README.md)  
- Lista containers ativos e inativos.
- Para e remove containers.

### 4. [Dockerfile para aplicação Flask](Exercicio04/README.md)  
- Criação de uma imagem Docker com Python e Flask.
- Responde a uma rota simples.

---

## 🟡 Médio

### 5. [Volumes com MySQL](Exercicio05/README.md)  
- Cria um volume para armazenar dados persistentes do banco MySQL.

### 6. [Multi-stage build com Go](Exercicio06/README.md)  
- Cria um build otimizado de uma aplicação Go usando múltiplos estágios.

### 7. [Rede Docker com Node.js e MongoDB](Exercicio07/README.md)  
- Cria uma rede personalizada.
- Faz comunicação entre containers.

### 8. [Compose file com PostgreSQL e pgAdmin](Exercicio08/README.md)  
- Usa Docker Compose para gerenciar uma aplicação com banco de dados e interface gráfica.

---

## 🔴 Difícil

### 9. [Imagem personalizada com Nginx ou Apache](Exercicio09/README.md)  
- Objetivo: Criar uma imagem baseada no Nginx ou Apache para hospedar arquivos HTML/CSS estáticos.
- Descrição:
  - Utilize a landing page do [Creative Tim](https://www.creative-tim.com/) como conteúdo estático.
  - Configure o `Dockerfile` para copiar os arquivos da landing page para o diretório padrão do servidor web.
  - Construa e execute o container, expondo-o na porta 8080 para acessar a página no navegador.

### 10. [Evitar execução como root](Exercicio10/README.md)  
- Objetivo: Configurar um Dockerfile para executar um container com um usuário não-root.
- Descrição:
  - Crie um usuário no `Dockerfile` com `useradd` ou `adduser`.
  - Defina esse usuário como padrão usando a instrução `USER`.
  - Construa a imagem e inicie o container.
  - Verifique se o processo está rodando com o novo usuário utilizando:
    ```bash
    docker exec <container> whoami
    ```

### 11. [Análise de vulnerabilidades com Trivy](Exercicio11/README.md)  
- Objetivo: Utilizar o Trivy para identificar vulnerabilidades em imagens Docker públicas.
- Descrição:
  - Instale o Trivy em sua máquina.
  - Analise uma imagem pública, como `python:3.9` ou `node:16`.
  - Filtre vulnerabilidades com severidade **HIGH** ou **CRITICAL**.
  - Documente os pacotes ou bibliotecas afetadas e sugira possíveis ações, como atualização da imagem base ou substituição de dependências.

### 12. [Corrigir vulnerabilidades encontradas](Exercicio12/README.md)  
- Objetivo: Aplicar melhorias em um Dockerfile vulnerável, seguindo boas práticas de segurança.
- Descrição:
  - Trabalhe com um exemplo de Dockerfile que utiliza uma imagem base genérica e executa como usuário root.
  - Identifique melhorias, como:
    - Substituir a imagem base por uma versão mais enxuta.
    - Criar um usuário não-root.
    - Remover bibliotecas desnecessárias e limpar o cache.
  - Gere um novo Dockerfile mais seguro e otimizado.

---

## 📸 Capturas de Tela

As capturas de tela dos testes e execuções estão localizadas nas respectivas pastas dos exercícios.

---

## 🧑‍💻 Autor

Feito por Rogério 🚀  
[LinkedIn](https://www.linkedin.com/in/rogerio-de-lima-rodrigues/)

---

## 📄 Licença

Este projeto está licenciado sob a licença MIT. Veja o arquivo [LICENSE](./LICENSE) para mais detalhes.
