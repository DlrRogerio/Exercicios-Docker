# Analisando Imagem Docker com Trivy

Neste exercício, utilizaremos o Trivy, uma ferramenta open source para análise de vulnerabilidades, para escanear uma imagem Docker pública em busca de vulnerabilidades conhecidas.

---

## Passos para Realizar a Análise

### 1. Instalar o Trivy
Instale o Trivy na sua máquina utilizando o seguinte comando:

```bash
curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin
```

Após a instalação, verifique se o Trivy foi instalado corretamente:

```bash
trivy --version
```

---

### 2. Analisar a Imagem Docker
Utilize o Trivy para analisar a imagem Docker pública `python:3.9`. O comando abaixo filtra apenas vulnerabilidades com severidade **HIGH** e **CRITICAL**, e salva o resultado no formato JSON em um arquivo chamado `vulnerabilidades-python39.json`:

```bash
trivy image --severity HIGH,CRITICAL --format json -o vulnerabilidades-python39.json python:3.9
```

**Explicação do Comando:**
- `trivy image`: Indica que você está analisando uma imagem Docker.
- `--severity HIGH,CRITICAL`: Filtra vulnerabilidades com severidade alta ou crítica.
- `--format json`: Define o formato da saída como JSON.
- `-o vulnerabilidades-python39.json`: Salva o resultado no arquivo especificado.
- `python:3.9`: Nome da imagem Docker a ser analisada.

---

### 3. Identificar Vulnerabilidades
Após a análise, abra o arquivo `vulnerabilidades-python39.json` para revisar as vulnerabilidades detectadas. Você pode utilizar comandos como `cat` ou abrir o arquivo em um editor de texto.

```bash
cat vulnerabilidades-python39.json
```

Procure por vulnerabilidades com severidade **HIGH** ou **CRITICAL** e note os seguintes detalhes:
- **Nome do Pacote/Biblioteca** afetado.
- **Descrição da vulnerabilidade**.
- **Possíveis ações** para mitigar o risco.

---

### 4. Sugerir Ações para Mitigação
Com base nas vulnerabilidades encontradas, considere as seguintes ações:
1. **Atualização da Imagem Base:** Verifique se há uma versão mais recente da imagem base (`python:3.9`) que corrige as vulnerabilidades.
   ```bash
   docker pull python:3.9
   ```
2. **Substituição de Dependências:** Identifique bibliotecas ou pacotes vulneráveis e considere substituí-los ou removê-los, se possível.
3. **Aplicação de Patches:** Caso a vulnerabilidade seja relacionada a um pacote específico, verifique se há patches de segurança disponíveis.

---

### Exemplo de Mitigação
Se o Trivy identificar uma vulnerabilidade crítica em um pacote como `libssl`, a mensagem poderá incluir:
- **Nome do Pacote:** libssl
- **Descrição:** Vulnerabilidade relacionada à criptografia.
- **Ação Recomendada:** Atualizar o pacote ou substituir por uma versão corrigida.

---

## Observações Finais
- O Trivy é uma ferramenta poderosa para manter imagens Docker mais seguras.
- Sempre revise e atualize suas imagens regularmente para minimizar riscos de segurança.
- Considere automatizar a análise com Trivy em pipelines CI/CD para verificar vulnerabilidades antes de implantar novas imagens.

Agora você está pronto para analisar e mitigar vulnerabilidades em imagens Docker utilizando o Trivy!
