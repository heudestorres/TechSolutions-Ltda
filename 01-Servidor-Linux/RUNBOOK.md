# Runbook - Projeto 01

## Objetivo

Documentar os procedimentos realizados durante a implantação do servidor Ubuntu.

---

# Etapa 1 - Instalação

- Download da ISO
- Criação da máquina virtual
- Instalação do Ubuntu Server
- Configuração inicial

---

# Etapa 2 - Sistema de Arquivos

Comandos utilizados:

- pwd
- ls
- cd
- tree

Objetivo:

Compreender a estrutura do sistema Linux.

---

# Etapa 3 - Usuários

Comandos utilizados

- adduser
- passwd
- usermod
- groups
- id

---

# Etapa 4 - Permissões

Comandos

- chmod
- chown
- ls -l

---

# Etapa 5 - systemd

Comandos

- systemctl status
- systemctl restart
- systemctl enable

---

# Etapa 6 - Processos

Comandos

- ps
- top
- htop
- kill

---

# Etapa 7 - Logs

Comandos

- journalctl
- ls /var/log

---

# Etapa 8 - Pacotes

Comandos

- apt update
- apt install
- apt remove

---

# Etapa 9 - Configuração de Rede

## Objetivo

Configurar o servidor com endereço IP estático para garantir que os serviços permaneçam acessíveis mesmo após reinicializações.

---

## Backup do arquivo

```bash
sudo cp /etc/netplan/00-installer-config.yaml \
/etc/netplan/00-installer-config.yaml.bkp
```

---

## Editar o Netplan

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

Foi configurado:

- IP estático
- Gateway padrão
- DNS
- Interface ens33

---

## Validar configuração

```bash
sudo netplan try
```

---

## Aplicar configuração

```bash
sudo netplan apply
```

---

## Testes realizados

```bash
ip a
```

```bash
ip route
```

```bash
ping -c 4 192.168.1.254
```

```bash
ping -c 4 google.com
```

---

## Resultado esperado

- Interface ens33 ativa
- IP 192.168.1.50
- Gateway 192.168.1.254
- DNS funcionando
- Conectividade com Internet validada
