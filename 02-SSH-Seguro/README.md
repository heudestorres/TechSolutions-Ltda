
# Projeto 02 - SSH Seguro

## Objetivo

Implementar e configurar o OpenSSH Server em um servidor Ubuntu, aplicando controles de segurança para proteger o acesso remoto e reduzir a superfície de ataque.

O projeto simula a implementação de acesso remoto seguro em um ambiente corporativo da empresa fictícia **TechSolutions Ltda.**, utilizando autenticação por chaves SSH, restrição de usuários e políticas de hardening.

---

## Cenário

O servidor Ubuntu da TechSolutions Ltda. possui endereço IP estático e está conectado à rede local.

O acesso administrativo é realizado remotamente a partir de uma estação Windows utilizando o protocolo SSH.

Após a validação do acesso remoto, foram aplicadas configurações de segurança para restringir usuários autorizados, impedir o login direto do usuário root e desabilitar a autenticação por senha.

---

## Tecnologias

- Ubuntu Server 26.04 LTS
- OpenSSH Server
- OpenSSH Client para Windows
- SSH
- Chaves SSH ED25519
- systemd
- VMware Workstation

---

## Arquitetura

```text
┌──────────────────────────────┐
│ Estação Administrativa       │
│ Windows                      │
│ OpenSSH Client               │
│ IP: 192.168.1.64             │
└──────────────┬───────────────┘
               │
               │ SSH - Porta 22
               │ Autenticação por chave
               │
┌──────────────▼───────────────┐
│ Ubuntu Server                │
│ Hostname: infra-server       │
│ IP: 192.168.1.50             │
│ OpenSSH Server               │
└──────────────────────────────┘
