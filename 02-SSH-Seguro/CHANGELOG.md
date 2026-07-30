# Changelog

Todas as alterações relevantes deste projeto são registradas neste arquivo.

---

## v0.1

### Adicionado

- Criação da estrutura inicial do Projeto 02.
- Criação das pastas `docs`, `imagens` e `scripts`.
- Criação dos arquivos de documentação:
  - `README.md`
  - `RUNBOOK.md`
  - `CHANGELOG.md`
  - `LESSONS_LEARNED.md`

---

## v0.2

### Adicionado

- Verificação do serviço OpenSSH Server.
- Validação do funcionamento do serviço SSH.
- Verificação da porta TCP 22 em estado de escuta.
- Realização do primeiro acesso remoto ao Ubuntu Server a partir do Windows.
- Validação da sessão remota utilizando os comandos `who` e `w`.

---

## v0.3

### Adicionado

- Geração de um par de chaves SSH utilizando o algoritmo ED25519.
- Configuração da autenticação por chave pública.
- Adição da chave pública ao arquivo `authorized_keys`.
- Configuração das permissões do diretório `.ssh`.
- Configuração das permissões do arquivo `authorized_keys`.
- Validação do acesso remoto utilizando autenticação por chave.

---

## v0.4

### Adicionado

- Backup do arquivo de configuração `sshd_config`.
- Desativação do login remoto direto do usuário `root`.
- Desativação da autenticação por senha.
- Habilitação da autenticação por chave pública.
- Restrição de acesso SSH utilizando `AllowUsers`.
- Limitação do número de tentativas de autenticação.
- Configuração de tempo limite para autenticação.
- Validação da sintaxe do arquivo `sshd_config`.
- Realização de testes de acesso autorizado e acesso negado.
- 
### Corrigido

- Ajustada a configuração `PasswordAuthentication` no arquivo `/etc/ssh/sshd_config.d/50-cloud-init.conf`.
- Resolvido o conflito entre o arquivo principal `sshd_config` e a configuração adicional gerenciada pelo cloud-init.
- Confirmada a desativação efetiva da autenticação por senha utilizando `sudo sshd -T`.

### Alterado

- Método de autenticação SSH alterado de senha para chave pública.
- Política de acesso remoto atualizada para permitir somente usuários autorizados.

### Segurança

- Redução da superfície de ataque do serviço OpenSSH.
- Bloqueio do login remoto direto do usuário `root`.
- Redução do risco de ataques de força bruta por meio da limitação de tentativas.
- Remoção da autenticação por senha.
- Restrição do acesso remoto por usuário.

---

## v1.0

### Concluído

- Implementação do acesso remoto seguro ao Ubuntu Server.
- Configuração da autenticação utilizando chaves SSH ED25519.
- Aplicação das políticas de hardening do OpenSSH.
- Validação dos controles de segurança implementados.
- Organização das evidências técnicas.
- Documentação completa do Projeto 02.
