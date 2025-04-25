# Exercício 02 - Criando e rodando um container interativo

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
    echo "⚠️  syslog não está disponível neste container. Tentando journalctl..."
    journalctl -n 10 2>/dev/null || echo "❌ journalctl também não disponível."
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
1. **Lista os arquivos no diretório `/var/log`**  
   Exibe uma listagem detalhada (`ls -lh`) para mostrar os arquivos de log disponíveis.

2. **Verifica e exibe o conteúdo de `/var/log/dpkg.log`**  
   - Se o arquivo existir, mostra as 10 primeiras linhas com `head -n 10`.  
   - Caso não exista, exibe uma mensagem de aviso.

3. **Verifica e exibe os últimos registros do syslog**  
   - Se o arquivo `/var/log/syslog` existir, mostra as últimas 10 linhas com `tail -n 10`.  
   - Se não existir, tenta buscar os 10 últimos registros do sistema com `journalctl -n 10`.  
   - Caso `journalctl` também não esteja disponível, exibe um aviso de indisponibilidade.

4. **Mensagem final**  
   Finaliza com uma mensagem indicando que o script foi executado com sucesso.


---

### 5. Executar o Script
Após criar o script, torne-o executável e execute-o:

```bash
chmod +x script.sh
./script.sh
```

---

## Resultados Esperados
- Listagem detalhada dos arquivos presentes no diretório `/var/log`.
- Exibição das 10 primeiras linhas do arquivo `/var/log/dpkg.log`, se o arquivo existir.
- Exibição dos últimos 10 registros do arquivo `/var/log/syslog`, se disponível.
- Caso o `syslog` não esteja disponível, exibição dos últimos 10 registros do sistema via `journalctl`, se instalado.
- Finalização com uma mensagem indicando a conclusão do script.

---

## Observações Finais
- Este container é temporário. Ao sair do container, ele será descartado, a menos que você tenha configurado o modo de persistência.
- Para garantir a persistência, utilize a flag `--name` ao criar o container ou salve as alterações em uma imagem.

Agora você tem um ambiente Ubuntu interativo configurado com Docker e um script de logs funcional!
