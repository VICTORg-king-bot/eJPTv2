# Descubrimiento de Red

Antes de atacar, debemos identificar los hosts activos en la red. Estas herramientas permiten descubrir dispositivos mediante pings y tablas ARP.

## ARP-SCAN

Escanea la red local usando peticiones ARP. Es rápido y fiable en entornos LAN.

```bash
ip a
# Identifica tu interfaz de red (eth0, wlan0, etc.)
```

```bash
sudo arp-scan -I eth0 --localnet
```

> Los sistemas virtualizados suelen tener MAC empezando por `08:00`.

## NETDISCOVER

Alternativa a arp-scan que también usa ARP para descubrir hosts.

```bash
sudo netdiscover -i eth0 -r 192.168.0.0/24
```

> El ultimo octeto debe ser `0/24` para indicar la mascara de red.

## NMAP (Ping Sweep)

Escaneo de descubrimiento sin necesidad de resolver nombres DNS.

```bash
nmap -sn 192.168.0.0/24 -oN ips_disponibles.txt
```

## Identificacion del Sistema Operativo por TTL

Al hacer ping a un host, el valor TTL ayuda a identificar el SO:

- **TTL ~128** -> Windows
- **TTL ~64** -> Linux

```bash
ping -c 1 <IP>
```

> El TTL puede reducirse si hay routers intermedios.
