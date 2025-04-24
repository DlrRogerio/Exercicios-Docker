# Criando e rodando um container interativo

Inicie um container Ubuntu e interaja com o terminal dele. Teste um script Bash que imprime logs do sistema ou instala pacotes de forma interativa.


---

## Passos para Configuração

### 1. Executar o Container Ubuntu
O comando abaixo cria e executa um container utilizando a imagem base do Ubuntu em modo interativo.

```bash
docker run -it ubuntu
```

**Explicação do Comando:**
- `docker run`: Cria e executa um container.
- `-i`: Ativa o modo interativo, mantendo o stdin aberto.
- `-t`: Aloca um terminal (TTY) para o container.
- `ubuntu`: Define a imagem base a ser utilizada. Caso não tenha a imagem localmente, o Docker fará o download.

---

### 2. Dentro do Container
Após executar o comando, o prompt será alterado para algo como:

```
root@<container_id>:/#
```

Agora você está dentro do container e pode utilizar comandos como:

```bash
apt update
apt install nano -y
nano script.sh
```

---

### 3. Criar um Script Bash
Crie um script chamado `script.sh` e cole o seguinte conteúdo:

```bash
#!/bin/bash

echo "📦 Atualizando lista de pacotes..."
apt update -y > /dev/null

echo "📥 Instalando o pacote 'logrotate' (opcional)..."
apt install logrotate -y > /dev/null

echo ""
echo "📂 Listando arquivos em /var/log:"
ls -lh /var/log

echo ""
echo "📄 Exibindo as 10 primeiras linhas de /var/log/dpkg.log (se existir):"
if [ -f /var/log/dpkg.log ]; then
    head -n 10 /var/log/dpkg.log
else
    echo "⚠️  Arquivo /var/log/dpkg.log não encontrado."
fi

echo ""
echo "📄 Exibindo os últimos 10 registros do syslog (se existir):"
if [ -f /var/log/syslog ]; then
    tail -n 10 /var/log/syslog
else
    echo "⚠️  syslog não está disponível neste container."
fi

echo ""
echo "✅ Fim do script de logs."
```

**Passos para Criar:**
1. Use o editor `nano` para criar o arquivo:  
   ```bash
   nano script.sh
   ```
2. Cole o conteúdo acima no editor.
3. Salve o arquivo pressionando `CTRL+O`, `Enter` e `CTRL+X`.

---

### 4. Explicação do Script
O script realiza as seguintes operações:
1. Atualiza a lista de pacotes (`apt update`).
2. Instala o pacote `logrotate` (opcional).
3. Lista os arquivos no diretório `/var/log`.
4. Exibe as 10 primeiras linhas do arquivo `/var/log/dpkg.log`, se existir.
5. Exibe os últimos 10 registros do syslog, se disponível.
6. Finaliza com uma mensagem de sucesso.

---

### 5. Executar o Script
Após criar o script, torne-o executável e execute-o:

```bash
chmod +x script.sh
./script.sh
```

---

## Resultados Esperados
- Atualização silenciosa da lista de pacotes e instalação do `logrotate`.
- Listagem de arquivos no diretório `/var/log`.
- Exibição das primeiras linhas de `/var/log/dpkg.log` (se existir).
- Exibição dos últimos registros do syslog (se disponível).

---

## Observações Finais
- Este container é temporário. Ao sair do container, ele será descartado, a menos que você tenha configurado o modo de persistência.
- Para garantir a persistência, utilize a flag `--name` ao criar o container ou salve as alterações em uma imagem.

Agora você tem um ambiente Ubuntu interativo configurado com Docker e um script de logs funcional!
