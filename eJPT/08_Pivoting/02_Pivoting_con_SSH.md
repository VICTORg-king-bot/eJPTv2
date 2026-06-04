# Pivoting con SSH (SSHuttle)

SSHuttle permite crear un tunel VPN sobre SSH para acceder a redes internas.

## Requisito: SSH en la Maquina Intermediaria

Si la maquina intermediaria es Linux y no tiene SSH:

```bash
sudo apt update
sudo apt install openssh-server -y
sudo systemctl enable ssh
sudo systemctl start ssh
```

## Verificar Interfaces de Red

```bash
hostname -I
```

Identificar la IP en modo puente (conectada a nuestra Kali) y la IP en la red interna.

## Pivoting con SSHuttle

```bash
sshuttle -r <usuario>@<IP_ubuntu> 10.10.10.0/24
```

- `<usuario>@<IP_ubuntu>` -> Credenciales de la maquina intermediaria
- `10.10.10.0/24` -> Rango de la red interna a la que queremos acceder

> SSHuttle crea un tunel automatico: todo el trafico hacia la red interna pasa a traves del SSH.

## Descubrir Hosts en la Red Interna

Desde la maquina intermediaria:

```bash
sudo arp-scan -I <interfaz_interna> --localnet
```

> Una vez configurado SSHuttle, podemos usar nmap, hydra, etc. directamente contra las IPs de la red interna desde nuestra maquina Kali.
