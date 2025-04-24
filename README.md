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

### 1. [Rodando um container básico (Nginx + TailwindCSS)](Exercicio01/README.md)  
- Executa um container com Nginx.
- Usa uma landing page do TailwindCSS como conteúdo estático.

### 2. [Container interativo com Ubuntu](Exercicio02/README.md)  
- Acessa terminal bash.
- Roda scripts e instala pacotes manualmente.

### 3. [Listando e removendo containers](Exercicio03/README.md)  
- Lista containers ativos e inativos.
- Para e remove containers.

### 4. [Dockerfile para aplicação Flask](Exercicio04/README.md)  
- Criação de uma imagem Docker com Python e Flask.
- Responde uma rota simples.

---

## 🟡 Médio

### 5. [Volumes com MySQL](Exercicio05/README.md)  
- Cria um volume para armazenar dados persistentes do banco MySQL.

### 6. [Multi-stage build com Go](Exercicio06/README.md)  
- Cria build otimizado de uma aplicação Go usando múltiplos estágios.

### 7. [Rede Docker com Node.js e MongoDB](Exercicio07/README.md)  
- Cria uma rede personalizada.
- Faz comunicação entre containers.

### 8. [Compose file com PostgreSQL e pgAdmin](Exercicio08/README.md)  
- Usa Docker Compose para gerenciar uma aplicação com banco e interface gráfica.

---

## 🔴 Difícil

### 9. [Imagem personalizada com Nginx ou Apache](Exercicio09/README.md)  
- Cria uma imagem com arquivos estáticos (HTML/CSS).
- Usa uma landing page moderna do Creative Tim.

### 10. [Evitar execução como root](Exercicio10/README.md)  
- Cria um usuário no Dockerfile.
- Define como usuário padrão com `USER`.

### 11. [Análise de vulnerabilidades com Trivy](Exercicio11/README.md)  
- Instala o Trivy.
- Analisa imagens públicas (ex: `python:3.9`, `node:16`).
- Identifica e sugere ações para vulnerabilidades HIGH/CRITICAL.

### 12. [Corrigindo vulnerabilidades](Exercicio12/README.md)  
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
