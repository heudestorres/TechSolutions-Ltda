# Lições Aprendidas

## Projeto 02 - SSH Seguro

Durante este projeto, aprendi a implementar e proteger o acesso remoto a um servidor Ubuntu utilizando o protocolo SSH.

---

## Objetivos alcançados

Durante este projeto aprendi a:

- Compreender o funcionamento do protocolo SSH.
- Diferenciar SSH de protocolos antigos e inseguros, como Telnet.
- Verificar o status do serviço OpenSSH utilizando o `systemctl`.
- Verificar se a porta TCP 22 está em escuta utilizando o comando `ss`.
- Realizar o acesso remoto ao Ubuntu Server a partir do Windows.
- Compreender o processo de verificação da identidade do servidor durante a primeira conexão.
- Utilizar o arquivo `known_hosts` para armazenar as identidades dos servidores acessados.
- Gerar um par de chaves SSH utilizando o algoritmo ED25519.
- Compreender a diferença entre chave pública e chave privada.
- Configurar a autenticação por chave pública.
- Utilizar o arquivo `authorized_keys` para autorizar o acesso de clientes SSH.
- Configurar as permissões corretas do diretório `.ssh` e do arquivo `authorized_keys`.
- Validar o acesso remoto utilizando autenticação por chave.
- Realizar o hardening do OpenSSH Server.
- Desabilitar o login remoto direto do usuário `root`.
- Desabilitar a autenticação por senha.
- Restringir o acesso SSH a usuários autorizados.
- Limitar o número de tentativas de autenticação.
- Configurar um tempo limite para a autenticação.
- Validar a sintaxe do arquivo `sshd_config` utilizando o comando `sshd -t`.
- Realizar testes positivos e negativos de acesso.
- Documentar as configurações e os controles de segurança implementados.

---

## Principais dificuldades

Durante a implementação, os principais pontos que exigiram mais atenção foram:

- Identificar por que a configuração `PasswordAuthentication no` não estava sendo aplicada.
- Compreender a influência dos arquivos adicionais localizados em `/etc/ssh/sshd_config.d/`.

---

## Como resolvi

Os desafios foram resolvidos por meio de:

- Utilização do comando `grep` para localizar todas as configurações relacionadas a `PasswordAuthentication`.
- Análise do arquivo `/etc/ssh/sshd_config.d/50-cloud-init.conf`.
- Verificação da configuração efetiva utilizando `sudo sshd -T`.
- Correção da configuração adicional do cloud-init e nova validação do serviço.
