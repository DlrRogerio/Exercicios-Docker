# Exercicios-Docker

Este repositório contém a resolução completa de uma lista de exercícios Docker, divididos em níveis de dificuldade: **Fácil**, **Médio** e **Difícil**. Cada exercício tem seus comandos explicados, capturas de tela (se necessário), e instruções de execução.

---

## ✅ Pré-requisitos

- Docker
- Docker Compose
- Git
- Trivy (para o exercício 11)
- Navegador para visualizar páginas web

---

## 🟢 Fácil

### 1. Rodando um container básico (Nginx + TailwindCSS)
- Executa um container com Nginx.
- Usa uma landing page do TailwindCSS como conteúdo estático.

### 2. Container interativo com Ubuntu
- Acessa terminal bash.
- Roda scripts e instala pacotes manualmente.

### 3. Listando e removendo containers
- Lista containers ativos e inativos.
- Para e remove containers.

### 4. Dockerfile para aplicação Flask
- Criação de uma imagem Docker com Python e Flask.
- Responde uma rota simples.

---

## 🟡 Médio

### 5. Volumes com MySQL
- Cria um volume para armazenar dados persistentes do banco MySQL.

### 6. Multi-stage build com Go
- Cria build otimizado de uma aplicação Go usando múltiplos estágios.

### 7. Rede Docker com Node.js e MongoDB
- Cria uma rede personalizada.
- Faz comunicação entre containers.

### 8. Compose file com PostgreSQL e pgAdmin
- Usa Docker Compose para gerenciar uma aplicação com banco e interface gráfica.

---

## 🔴 Difícil

### 9. Imagem personalizada com Nginx ou Apache
- Cria uma imagem com arquivos estáticos (HTML/CSS).
- Usa uma landing page moderna do Creative Tim.

### 10. Evitar execução como root
- Cria um usuário no Dockerfile.
- Define como usuário padrão com `USER`.

### 11. Análise de vulnerabilidades com Trivy
- Instala o Trivy.
- Analisa imagens públicas (ex: `python:3.9`, `node:16`).
- Identifica e sugere ações para vulnerabilidades HIGH/CRITICAL.

### 12. Corrigindo vulnerabilidades
- Melhora Dockerfile vulnerável.
- Aplica boas práticas de segurança e tamanho de imagem.

---

## 📸 Capturas de Tela

As capturas de tela dos testes e execuções estão localizadas nas respectivas pastas dos exercícios.

---

## 🧑‍💻 Autor

Feito por [Seu Nome Aqui] 🚀  
[Seu LinkedIn ou GitHub]

---

## 📄 Licença

Este projeto está licenciado sob a licença MIT. Veja o arquivo [LICENSE](./LICENSE) para mais detalhes.
