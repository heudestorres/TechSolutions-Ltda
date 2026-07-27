# Lessons Learned

## Projeto 01 - Ubuntu Server

### Objetivos alcançados

Durante este projeto aprendi a:

- Instalar um servidor Ubuntu Server do zero.
- Compreender a estrutura do sistema de arquivos Linux.
- Administrar usuários e grupos.
- Configurar permissões de arquivos e diretórios.
- Gerenciar serviços utilizando o systemd.
- Monitorar processos e recursos do sistema.
- Consultar e interpretar logs do Linux.
- Gerenciar pacotes utilizando o APT.
- Configurar um endereço IP estático utilizando Netplan.
- Configurar gateway e servidores DNS.
- Validar a conectividade da rede.
- Documentar tecnicamente todas as etapas do projeto.

---

## Principais dificuldades

- Memorizar as combinações numéricas utilizadas no comando `chmod`.
- Compreender a estrutura de indentação dos arquivos YAML durante a configuração do Netplan.

---

## Como resolvi

- Realizei diversos testes práticos utilizando diferentes permissões até compreender o funcionamento do `chmod`.
- Analisei as mensagens de erro do Netplan, corrigi a indentação do arquivo YAML e validei a configuração utilizando `netplan try` antes de aplicá-la definitivamente.

---

## Boas práticas aprendidas

- Sempre realizar backup de arquivos de configuração antes de modificá-los.
- Validar alterações antes de aplicá-las em produção.
- Testar a conectividade após alterações de rede.
- Documentar todas as mudanças realizadas.
- Organizar o projeto de forma padronizada para facilitar futuras manutenções.

---

## Próximos objetivos

No próximo projeto pretendo aprender:

- Funcionamento do protocolo SSH.
- Configuração segura do OpenSSH Server.
- Hardening de servidores Linux.
- Autenticação utilizando chaves públicas e privadas.
- Boas práticas de segurança utilizadas em ambientes corporativos.
