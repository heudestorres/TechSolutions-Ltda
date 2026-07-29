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

- Compreender a diferença entre a chave pública e a chave privada.
- Entender onde cada chave deve ser armazenada.
- Compreender o funcionamento do arquivo `authorized_keys`.
- Configurar corretamente as permissões do diretório `.ssh`.

---

## Como resolvi

Os desafios foram resolvidos por meio de:

- Estudo do funcionamento da autenticação assimétrica utilizada pelo SSH.
- Realização de testes práticos entre o Windows e o Ubuntu Server.
- Verificação do serviço SSH antes e depois das alterações.
- Análise das permissões do diretório `.ssh` e do arquivo `authorized_keys`.
- Validação da configuração utilizando o comando:

```bash
sudo sshd -t
