# Runbook - Projeto 02

## Objetivo

Documentar o procedimento de configuração e proteção do acesso remoto ao Ubuntu Server utilizando o OpenSSH.

O projeto inclui a validação do serviço, o primeiro acesso remoto, a autenticação por chaves SSH e a aplicação de controles de hardening.

---

# Etapa 1 - Validação do serviço OpenSSH

## Objetivo

Confirmar que o serviço SSH está instalado, ativo e disponível para conexões remotas.

---

## Verificar o status do serviço

```bash
sudo systemctl status ssh
```

### Resultado esperado

O serviço deve apresentar um estado semelhante a:

```text
Active: active (running)
```

---

## Verificar se o serviço inicia automaticamente

```bash
sudo systemctl is-enabled ssh
```

### Resultado esperado

```text
enabled
```

---

## Verificar a porta SSH

```bash
sudo ss -tulpn | grep :22
```

### Resultado esperado

O serviço deve estar em estado de escuta na porta TCP 22.

Exemplo:

```text
LISTEN 0 128 0.0.0.0:22
```

---

# Etapa 2 - Primeiro acesso remoto

## Objetivo

Validar o acesso remoto ao Ubuntu Server a partir da estação administrativa Windows.

---

## Conectar ao servidor

No PowerShell do Windows:

```powershell
ssh usuario@192.168.1.50
```

Substituir `usuario` pelo nome do usuário configurado no Ubuntu Server.

---

## Confirmar a identidade do servidor

Na primeira conexão, o cliente SSH poderá exibir uma mensagem semelhante a:

```text
The authenticity of host cannot be established.
Are you sure you want to continue connecting?
```

Digite:

```text
yes
```

A identidade do servidor será registrada no arquivo `known_hosts` do cliente.

---

## Validar a sessão remota

No Ubuntu Server:

```bash
who
```

ou:

```bash
w
```

### Resultado esperado

A sessão SSH deve aparecer como uma conexão remota ativa.

---

## Encerrar a sessão

```bash
exit
```

---

# Etapa 3 - Geração das chaves SSH

## Objetivo

Criar um par de chaves utilizando o algoritmo ED25519.

A chave privada permanecerá na estação Windows e a chave pública será adicionada ao servidor Ubuntu.

---

## Verificar se já existem chaves

No PowerShell:

```powershell
Get-ChildItem $HOME\.ssh
```

Verificar se já existem arquivos como:

```text
id_ed25519
id_ed25519.pub
```

---

## Gerar um novo par de chaves

```powershell
ssh-keygen -t ed25519 -C "usuario@infra-server"
```

Durante a criação:

- Pressionar `Enter` para utilizar o caminho padrão.
- Definir uma passphrase, caso desejado.
- Confirmar a criação dos arquivos.

---

## Arquivos criados

A chave privada será armazenada em:

```text
C:\Users\Usuario\.ssh\id_ed25519
```

A chave pública será armazenada em:

```text
C:\Users\Usuario\.ssh\id_ed25519.pub
```

> A chave privada não deve ser compartilhada, enviada ao servidor ou adicionada ao GitHub.

---

## Exibir a chave pública

```powershell
Get-Content $HOME\.ssh\id_ed25519.pub
```

A saída deve iniciar com:

```text
ssh-ed25519
```

---

# Etapa 4 - Configuração da autenticação por chave

## Objetivo

Adicionar a chave pública da estação Windows ao usuário autorizado no Ubuntu Server.

---

## Criar o diretório `.ssh`

No Ubuntu Server:

```bash
mkdir -p ~/.ssh
```

---

## Ajustar as permissões do diretório

```bash
chmod 700 ~/.ssh
```

---

## Adicionar a chave pública

Editar o arquivo:

```bash
nano ~/.ssh/authorized_keys
```

Adicionar a chave pública gerada no Windows em uma única linha.

Salvar o arquivo.

---

## Ajustar as permissões do arquivo

```bash
chmod 600 ~/.ssh/authorized_keys
```

---

## Verificar as permissões

```bash
ls -ld ~/.ssh
```

Resultado esperado:

```text
drwx------
```

Verificar o arquivo:

```bash
ls -l ~/.ssh/authorized_keys
```

Resultado esperado:

```text
-rw-------
```

---

## Testar a autenticação por chave

Encerrar a sessão SSH:

```bash
exit
```

No PowerShell:

```powershell
ssh usuario@192.168.1.50
```

### Resultado esperado

O acesso deve ser realizado utilizando a chave SSH.

Caso uma passphrase tenha sido configurada, será solicitada a passphrase da chave privada.

---

# Etapa 5 - Backup da configuração do OpenSSH

## Objetivo

Criar uma cópia de segurança do arquivo de configuração antes de aplicar as políticas de hardening.

---

## Criar o backup

```bash
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bkp
```

---

## Verificar o backup

```bash
sudo ls -l /etc/ssh/sshd_config*
```

---

# Etapa 6 - Hardening do OpenSSH

## Objetivo

Aplicar controles de segurança para reduzir a superfície de ataque do serviço SSH.

---

## Editar a configuração

```bash
sudo nano /etc/ssh/sshd_config
```

Adicionar ou ajustar as seguintes diretivas:

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
MaxAuthTries 3
LoginGraceTime 30
AllowUsers usuario
```

Substituir `usuario` pelo usuário autorizado a realizar o acesso SSH.

---

## Controles implementados

### `PermitRootLogin no`

Impede o login remoto direto utilizando o usuário `root`.

---

### `PasswordAuthentication no`

Desabilita a autenticação por senha.

---

### `PubkeyAuthentication yes`

Permite a autenticação utilizando chaves públicas.

---

### `MaxAuthTries 3`

Limita o número de tentativas de autenticação por conexão.

---

### `LoginGraceTime 30`

Define um limite de 30 segundos para a conclusão da autenticação.

---

### `AllowUsers usuario`

Restringe o acesso SSH aos usuários definidos.

---

# Etapa 7 - Validação da configuração

## Objetivo

Verificar se a configuração do OpenSSH possui erros antes de reiniciar o serviço.

---

## Validar a sintaxe

```bash
sudo sshd -t
```

### Resultado esperado

Nenhuma saída deve ser exibida.

A ausência de mensagens indica que nenhum erro de sintaxe foi encontrado.

---

## Reiniciar o serviço

```bash
sudo systemctl restart ssh
```

---

## Verificar o status

```bash
sudo systemctl status ssh
```

### Resultado esperado

```text
Active: active (running)
```

---

# Etapa 8 - Testes de segurança

## Objetivo

Validar o funcionamento dos controles implementados.

---

## Teste positivo

No PowerShell:

```powershell
ssh usuario@192.168.1.50
```

### Resultado esperado

O acesso deve ser realizado utilizando a chave SSH autorizada.

---

## Teste negativo - Usuário não autorizado

Tentar realizar o acesso utilizando um usuário diferente:

```powershell
ssh outro_usuario@192.168.1.50
```

### Resultado esperado

```text
Permission denied
```

---

## Teste negativo - Autenticação sem chave válida

Tentar acessar sem disponibilizar uma chave válida.

### Resultado esperado

A autenticação deve falhar, pois o login por senha está desabilitado.

---

# Etapa 9 - Verificação final

## Checklist

- [x] Serviço OpenSSH ativo.
- [x] Serviço configurado para iniciar automaticamente.
- [x] Porta TCP 22 em escuta.
- [x] Primeiro acesso remoto validado.
- [x] Chave SSH ED25519 criada.
- [x] Chave pública adicionada ao `authorized_keys`.
- [x] Permissões do diretório `.ssh` configuradas.
- [x] Permissões do `authorized_keys` configuradas.
- [x] Autenticação por chave validada.
- [x] Backup do `sshd_config` criado.
- [x] Login direto do `root` desabilitado.
- [x] Autenticação por senha desabilitada.
- [x] Usuários autorizados definidos.
- [x] Configuração validada com `sshd -t`.
- [x] Serviço SSH reiniciado sem erros.
- [x] Teste de acesso autorizado concluído.
- [x] Teste de acesso não autorizado concluído.
