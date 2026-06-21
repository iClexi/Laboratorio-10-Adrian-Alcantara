<div align="center">

# Laboratorio 10 - Issabel 5 en Rocky Linux

### Instalacion y configuracion de central telefonica IP con extensiones SIP y pruebas desde softphone.

![Platform](https://img.shields.io/badge/Platform-Rocky%20Linux-10B981?logo=rockylinux&logoColor=white)
![PBX](https://img.shields.io/badge/PBX-Issabel%205-blue)
![VoIP](https://img.shields.io/badge/VoIP-SIP%20%7C%20RTP-orange)
![Cloud](https://img.shields.io/badge/Cloud-DigitalOcean-0080FF?logo=digitalocean&logoColor=white)
![Topic](https://img.shields.io/badge/Topic-Telephony%20Server-purple)

</div>

---

## Descripcion

Este repositorio documenta una practica de instalacion y configuracion de Issabel 5 sobre Rocky Linux en un servidor cloud. La guia incluye preparacion del sistema, instalacion de la central, creacion de extensiones SIP y validacion desde un softphone.

## Practica incluida

| Archivo | Tema |
| --- | --- |
| `Practica 1 - Instalacion y Configuracion de Issabel.md` | Instalacion de Issabel 5, configuracion inicial, extensiones SIP y pruebas |

## How-To: usar el laboratorio

1. Crea un servidor Rocky Linux en DigitalOcean o un entorno equivalente.
2. Conectate por SSH como `root` o con un usuario con permisos `sudo`.
3. Sigue la guia principal paso a paso.
4. Abre los puertos necesarios para SIP y RTP.
5. Crea extensiones en Issabel.
6. Registra las extensiones desde un softphone.
7. Realiza una llamada de prueba entre extensiones.

## Requisitos

- Rocky Linux.
- Servidor con IP publica o red accesible.
- Acceso SSH.
- Navegador web para entrar al panel de Issabel.
- Softphone compatible con SIP.
- Puertos SIP y RTP permitidos en firewall.

## Puertos comunes

| Servicio | Puerto |
| --- | --- |
| SSH | 22/TCP |
| HTTP | 80/TCP |
| HTTPS | 443/TCP |
| SIP | 5060/UDP |
| RTP | 10000-20000/UDP |

## Comandos clave

```bash
ssh root@TU_IP_PUBLICA
yum update -y
hostnamectl set-hostname issabel.local
firewall-cmd --list-all
systemctl status asterisk
```

## Estructura del repositorio

```text
Laboratorio-10-Adrian-Alcantara/
├── Practica 1 - Instalacion y Configuracion de Issabel.md
└── README.md
```

## Resultado esperado

Al finalizar, Issabel debe quedar accesible por navegador, con extensiones SIP creadas y registradas correctamente en un softphone para realizar llamadas de prueba.
