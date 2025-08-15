ISSABEL 5 EN ROCKY LINUX (DIGITALOCEAN) – PASO A PASO
====================================================

Este archivo reúne todos los pasos para instalar y probar Issabel 5 en Rocky Linux,
crear extensiones SIP y registrar un softphone. Copia/pega tal cual.


0) DATOS QUE VAS A USAR
-----------------------
- IP pública del servidor (Droplet): TU_IP_PUBLICA
- Usuario SSH inicial: root (o un usuario con sudo)
- Extensiones a crear: 2221 y 2220
- Secret (password de ambas extensiones): Teletubies123$
- Puerto SIP por defecto: 5060/UDP
- Rango RTP por defecto: 10000–20000/UDP


1) CONEXIÓN SSH Y PREPARACIÓN DEL SISTEMA
-----------------------------------------
# Conéctate por SSH
ssh root@TU_IP_PUBLICA

# Actualiza paquetes
yum update -y

# Instala utilidades básicas
yum install -y wget curl

# (Opcional) Si usas firewalld y no está instalado/activo
# yum install -y firewalld
# systemctl enable --now firewalld


2) DESCARGAR Y EJECUTAR NETINSTALL DE ISSABEL 5
-----------------------------------------------
# Descarga el script de netinstall
wget http://repo.issabel.org/issabel5-netinstall.sh

# Dale permisos y ejecútalo
chmod +x issabel5-netinstall.sh
./issabel5-netinstall.sh

Durante el instalador:
- Elige Asterisk 16 o 18 (ambas son válidas).
- Define una contraseña para MariaDB (guárdala).
- Crea el usuario/contraseña del portal web (GUI de Issabel).
Al finalizar, el instalador puede reiniciar o pedirte reiniciar el servidor.


3) DETENER FAIL2BAN (PARA EVITAR BANEOS DURANTE PRUEBAS)
--------------------------------------------------------
# Vuelve a entrar por SSH si se reinició
ssh root@TU_IP_PUBLICA

# Detén Fail2ban
systemctl stop fail2ban

# (Opcional) Deshabilitarlo al arranque SOLO mientras pruebas
systemctl disable fail2ban

* Importante: por seguridad, recuerda re-habilitarlo cuando termines las pruebas:
# systemctl enable --now fail2ban


4) (RECOMENDADO) ABRIR PUERTOS EN FIREWALLD PARA PRUEBAS
--------------------------------------------------------
# HTTP/HTTPS para la GUI
firewall-cmd --add-service=http --permanent
firewall-cmd --add-service=https --permanent

# SIP y RTP (chan_sip por defecto)
firewall-cmd --add-port=5060/udp --permanent
firewall-cmd --add-port=10000-20000/udp --permanent

# Aplica cambios
firewall-cmd --reload

* Nota: Evita dejar 5060/UDP y RTP expuestos a todo internet.
  Idealmente usa VPN o limita por IP mientras haces pruebas.


5) ACCESO A LA GUI WEB DE ISSABEL
---------------------------------
Desde el navegador en tu PC/Host, abre:
http://TU_IP_PUBLICA
o
https://TU_IP_PUBLICA

Inicia sesión con el usuario/contraseña que definiste en el instalador.


6) CREAR EXTENSIONES 2221 Y 2220 (GENERIC SIP DEVICE)
-----------------------------------------------------
Ruta en Issabel:
PBX -> PBX Configuration -> Extensions

- En “Add Extension”, elige: Generic SIP Device
- Crea la extensión 2221 con:
  User Extension: 2221
  Display Name: Ext 2221
  secret (password): Teletubies123$
  nat: yes (si el teléfono está detrás de NAT)
  Submit y luego Apply Config (arriba)

- Repite el proceso para la extensión 2220:
  User Extension: 2220
  Display Name: Ext 2220
  secret (password): Teletubies123$
  nat: yes
  Submit y luego Apply Config


7) CONFIGURAR SOFTPHONE (ZOIPER / MICROSIP / OTRO) EN EL MÓVIL
--------------------------------------------------------------
En la app del softphone:
- Protocolo: SIP
- Usuario: 2221
- Contraseña: Teletubies123$
- Servidor/Domain/Host: TU_IP_PUBLICA
- Puerto: 5060 (UDP)

Guarda y registra. Deberías ver el registro en “verde”.


8) PRUEBAS RÁPIDAS
------------------
- Llama desde 2221 a 2220 para verificar registro y audio.
- Marca *43 (Echo Test) para probar envío/recepción de audio.

Si hay problemas de audio de un solo lado (one-way audio),
revisa el firewall y la NAT.


9) COMANDOS ÚTILES (SSH)
------------------------
# Mostrar IP
ip addr show

# Entrar a la consola de Asterisk
asterisk -rvvvvv

# Si usaste “Generic SIP Device” (chan_sip)
sip show peers

# Si creaste endpoints PJSIP (no aplica a “Generic SIP Device”)
pjsip show endpoints


10) NOTAS DE SEGURIDAD
----------------------
- No dejes Fail2ban desactivado en producción. Reactívalo cuando termines:
  systemctl enable --now fail2ban

- Limita el acceso a SIP/RTP por IP o usa VPN para evitar ataques de fuerza bruta.
- Cambia el secret por uno robusto si vas a dejar el sistema expuesto.
- Mantén el sistema y paquetes actualizados.
