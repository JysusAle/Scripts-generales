# Guía Práctica CCNA

## Información General

Este documento es una guía del curso CCNA con los siguientes módulos:

1. Introducción
2. Switching y Routing
3. Security y Automatización

### Materiales Necesarios

- 3 cables Ethernet
- 1 cable consola
- 1 cable USB serial
- Instalar Putty
- Instalar Packet Tracer
- Adaptador Ethernet a USB (si es necesario)

> Se debe firmar el reglamento, realizar exámenes por módulo y entregar un feedback al finalizar cada uno.

---

## Módulo 1 – Introducción

### ¿Qué es una Red de Datos?

Una red de datos está compuesta por:

- **Dispositivos finales**
- **Dispositivos intermedios** (switches y routers)
- **Estándares y protocolos**
- **Señales** que viajan por cables

### Tipos de Redes

| Tipo | Nombre | Estándar/Cable |
|------|--------|----------------|
| **LAN** | Local Area Network | Cable Ethernet, protocolo 802.3 |
| **WAN** | Wide Area Network | Fibra óptica, protocolos PPP y HDLC |

> **Nota:** El broadcast en WAN no existe.

### Tipos de Fibra Óptica

Existen dos tipos de fibra óptica: **monomodo** y **multimodo**. Se diferencian por sus colores.

### Tipos de Mensajes

- **Unicast:** Mensaje de uno a uno
- **Multicast:** Mensaje hacia muchos
- **Broadcast:** Mensaje hacia todos los dispositivos de la red

### Topologías

- **Física:** Indica cómo están montados los dispositivos en un rack
- **Lógica:** Indica cómo están conectados los dispositivos, en qué interfaz, con qué cables y con cuáles dispositivos

### Tipos de Puerto

- **FFA (Fast Ethernet):** 100 Mbps por puerto
- **GE (Gigabit Ethernet):** 1 Gbps por puerto

### Tipos de Cable

- Cable Ethernet directo
- Cable Ethernet cruzado
- Cable serial

---

### Internet

Red de datos que engloba LAN y WAN.

| Tipo | Descripción |
|------|-------------|
| **Internet público** | Acceso abierto |
| **Extranet** | Proveedores y clientes |
| **Intranet** | Red privada y local |
| **VPN** | Traslada virtualmente desde internet hacia una intranet |

> Un **sitio indexado** es aquel que aparece en resultados de búsqueda.

---

### Arquitectura de la Red

Son los requisitos (buenas prácticas) que debe tener una topología correcta:

1. **Tolerancia a fallos:** La topología debe ser redundante; si cae un cable, debe haber otro camino disponible.
2. **Calidad del servicio:** Que funcione correctamente cuando sea necesario.
3. **Escalabilidad:** Que acepte cambios a futuro.
4. **Seguridad:** No es posible al 100%, pero se debe maximizar:
   - **Autorización:** Lo que se tiene permitido hacer
   - **Autenticación:** Demostrar quién se dice ser (por lo que se sabe, lo que se tiene, o lo que se es)
   - **Disponibilidad:** La red debe estar accesible en todo momento
   - **Integridad:** La información no debe ser alterada; si lo es, debe ser rechazada
   - **Confidencialidad:** El mensaje solo es entendido por el receptor

---

### Modelo OSI

| # | Capa | Elementos clave |
|---|------|-----------------|
| 1 | **Física** | Bits, cables, hubs |
| 2 | **Enlace de datos** | Switches, ARP, tramas (frames), Ethernet, HDLC |
| 3 | **Red** | Routers, enrutamiento, NAT, paquetes, mejor ruta |
| 4 | **Transporte** | TCP, UDP, servicios |
| 5 | **Sesión** | Sistema operativo, inicio y fin de sesión |
| 6 | **Presentación** | Cifrado, lenguaje de programación, codificación |
| 7 | **Aplicación** | Interacción con el usuario |

---

### Modelo TCP/IP

| Capa TCP/IP | Equivalente OSI |
|-------------|-----------------|
| 1 – Acceso a la red | Capa 1 (Física) + Capa 2 (Enlace de datos) |
| 2 – Internet | Capa 3 (Red) |
| 3 – Transporte | Capa 4 (Transporte) |
| 4 – Aplicación | Capas 5, 6 y 7 (Sesión, Presentación, Aplicación) |

> Un **suite de protocolos** son todos los protocolos que se pueden usar en una red de datos.

---

### Conexión de Cables

| Tipo de cable | Conexión |
|---------------|----------|
| **Consola** | Computadora → Dispositivo |
| **Directo** | Computadora → Switch / Switch → Router |
| **Cruzado** | Switch → Switch / Router → Router / Computadora → Router |
| **Serial** | Router → Router |

---

### Protocolo Ethernet

- Utiliza el estándar **802.3**
- Existe el **broadcast**
- Usa **CSMA/CD** (Acceso múltiple con detección de colisiones)

**Hub:**
- Si falla un puerto, cae toda la red
- No tiene memoria
- Muy propenso a colisiones
- Trabaja en **half-duplex** (envía o recibe, no ambos al mismo tiempo)

**Switch:**
- Tiene memoria RAM
- Las colisiones son por interfaz (si falla un puerto, los demás siguen)
- Trabaja en **full-duplex** (envía y recibe al mismo tiempo)

> Los cables WAN no tienen colisiones ya que no usan protocolo Ethernet.

---

### Dirección MAC

- Dirección física de 48 bits en hexadecimal
- En Windows: `ipconfig /all`
- En Linux: `ifconfig`

---

### Dirección IP

Identificador de cada equipo en la red. IPv4 consta de 32 bits escritos en decimal, separados en 4 octetos, definidos por una máscara de red.

- La **máscara de red** indica cuántos bits pertenecen al segmento de red y cuántos a la porción host.

---

### Formas de Administración de un Equipo Cisco

1. Consola
2. Auxiliar
3. Líneas virtuales (VTY)

---

### Comandos Básicos en Terminal

```bash
# Entrar a modo privilegiado
enable

# Ver versión del equipo
show version

# Ver configuración activa
show running-config

# Entrar a modo configuración global
configure terminal

# Cambiar nombre del dispositivo
hostname <nombre>

# Contraseña modo privilegiado
enable password <contraseña>

# Crear usuario
username <nombre> password <contraseña>

# Configurar puerto consola
line console 0
login local

# Guardar configuración
copy running-config startup-config
# o también:
write

# Reiniciar dispositivo
reload
```

### Configurar Dirección IP en una Interfaz (Router)

```bash
interface gi0/0/0
ip address <dirección_IP> <máscara>
no shutdown
```

### Configurar Telnet

```bash
# Crear usuario y contraseña
username <nombre> password <contraseña>
enable password <contraseña>

# Habilitar líneas virtuales
line vty 0 15
login local
transport input telnet
exit

# Asignar IP a la interfaz
interface gi0/0/0
ip address <IP> <máscara>
no shutdown
```

```bash
# Conectarse por Telnet desde otra PC
telnet 192.168.0.3
```

### Configurar IP en un Switch (VLAN 1)

```bash
interface vlan 1
ip address <IP> <máscara>
no shutdown
```

---

### Direccionamiento IPv4

IPv4 consta de 32 bits divididos en 4 octetos.

#### Clases con Dirección

| Clase | Rango | Prefijo |
|-------|-------|---------|
| A | 0.0.0.0 – 127.0.0.0 | /8 |
| B | 128.0.0.0 – 191.255.0.0 | /16 |
| C | 192.0.0.0 – 223.255.255.0 | /24 |
| D | 224.0.0.0 en adelante | Multicast |

#### Direcciones IP Privadas

| Clase | Rango |
|-------|-------|
| A | 10.0.0.0 – 10.255.255.255 |
| B | 172.16.0.0 – 172.31.255.255 |
| C | 192.168.0.0 – 192.168.255.255 |

> - La IP de **broadcast** no se configura.
> - Las IPs privadas se configuran en intranets; desde fuera no deben ser accesibles.
> - **NAT:** Traduce una IP privada a una pública.
> - **Gateway:** Dirección que permite salir a otra red; la tiene el router y debe estar dentro del mismo segmento de red.

```bash
# Configurar gateway en un switch
ip default-gateway <dirección>
```

#### Tipos de Contraseña

| Tipo | Descripción |
|------|-------------|
| 0 | Texto en claro |
| 5 | Hash MD5 (`secret`) |
| 7 | Cifrado Cisco (`service password-encryption`) |

---

### VLSM (Variable Length Subnet Mask)

Se usa para no desperdiciar direcciones IP. La máscara varía según las necesidades.

**Pasos para hacer VLSM:**
1. Ordenar las redes de mayor a menor número de hosts
2. Sumar +2 a cada red (dirección de red + broadcast)
3. Particionar el segmento de red según las necesidades

---

### Enrutamiento

Proceso de elegir la mejor ruta para enviar paquetes entre redes.

#### RIP (Routing Information Protocol)

```bash
router rip
version 2
network <red>
network <red>
network <red>
```

> - **Red remota:** Red que no está conectada directamente al router.

---

### ARP (Address Resolution Protocol)

- Pertenece a la capa 2
- Objetivo: Conocer la MAC de destino
- Usa mensaje de **broadcast**
- MAC por defecto: `FF:FF:FF:FF:FF:FF`

---

### ICMP (Internet Control Message Protocol)

- Capa 3
- Verifica comunicación entre dispositivos
- Usa mensaje **unicast** (ping)
- Es de ida y vuelta

#### Comandos útiles en el Switch

```bash
# Ver tabla de MACs
show mac address-table

# Limpiar tabla de MACs
clear mac address-table dynamic

# Ver tabla de enrutamiento
show ip route
```

---

### Tipos de Enrutamiento

- **Estático:** Se configuran manualmente las rutas remotas
- **Dinámico:** Usa protocolos como RIP, OSPF o EIGRP

#### Distancia Administrativa (grado de confiabilidad)

| Protocolo | Distancia |
|-----------|-----------|
| Estático | 1 |
| EIGRP | 90 / 170 |
| OSPF | 110 |
| RIP | 120 |

#### Métrica (cómo el protocolo calcula la mejor ruta)

| Protocolo | Métrica |
|-----------|---------|
| RIP | Saltos |
| OSPF | Costo |
| EIGRP | Distancia factible |

---

### Capa de Transporte

#### TCP vs UDP

| Característica | TCP | UDP |
|----------------|-----|-----|
| Confiabilidad | Alta | Baja |
| Velocidad | Más lento | Más rápido |
| Reenvío de datos perdidos | Sí | No |

#### Puertos Comunes

| Protocolo | Puerto |
|-----------|--------|
| HTTP | 80 |
| HTTPS | 443 |
| FTP | 20 y 21 |
| SMTP | 25 |
| DNS | 53 |
| SSH | 22 |
| Telnet | 23 |
| DHCP | 67 y 68 |
| TFTP | 69 |

> **Socket:** Conexión entre cliente y servidor usando IP + número de puerto.

---

### HTTP y HTTPS

| | HTTP | HTTPS |
|-|------|-------|
| Puerto | 80 | 443 |
| Seguridad | No seguro | Seguro (TLS/SSL) |
| Certificado digital | No | Sí |

---

### DNS

- Puerto 53
- Configura dominios y alias asociados a una IP

---

### DHCP

- Si no hay broadcast, no funciona
- Proceso **DORA:**
  1. **Discover:** El cliente busca un servidor DHCP
  2. **Offer:** El servidor ofrece un direccionamiento
  3. **Request:** El cliente confirma que acepta la oferta
  4. **Acknowledge:** El servidor confirma y guarda el registro

```bash
# Configurar DHCP en un router
ip dhcp pool <NOMBRE_POOL>
network <DIRECCIÓN_DE_RED> <MÁSCARA>
default-router <GATEWAY>
dns-server <SERVIDOR_DNS>

# Excluir direcciones del pool
ip dhcp excluded-address <IP>
```

---

### FTP

| Comando | Acción |
|---------|--------|
| `dir` | Listar archivos |
| `get` | Descargar |
| `put` | Cargar |
| `rename` | Renombrar |
| `delete` | Eliminar |
| `quit` | Salir |

---

### SMTP

Un MUA (cliente de correo) envía un mensaje al servidor SMTP. Este verifica en la base de datos si el usuario existe en el dominio; si no, pasa el mensaje a otros servidores.

---

### Direccionamiento IPv6

- Consta de **128 bits** divididos en 8 segmentos separados por `:`
- No hay broadcast
- A la máscara se le llama **prefijo**

#### Tipos de Direcciones IPv6

| Tipo | Rango |
|------|-------|
| Unicast global | 2000::/3 a FFFF::/3 |
| Link-local | FE80::/10 |
| Multicast | FF00::/8 |

#### Reglas para Sintetizar IPv6

1. Quitar ceros a la izquierda en cada segmento
2. Si un segmento tiene todos ceros, se reemplaza por `0`
3. La regla `::` (doble dos puntos) solo se aplica **una vez**

> **NAT64:** Traducción de IPv4 a IPv6.

#### Configurar IPv6 en una Interfaz

```bash
ipv6 unicast-routing
interface gigabitEthernet 0/x/y
ipv6 address <DIRECCIÓN_IPv6>/<PREFIJO>
no shutdown
exit
```

#### Configurar IPv6 con EUI-64

```bash
ipv6 unicast-routing
interface gigabitEthernet 0/x/y
ipv6 address <DIRECCIÓN_IPv6>/<PREFIJO> eui-64
no shutdown
exit
```

---

### SSH (Secure Shell)

- Puerto **22**
- Servicio para conexiones remotas seguras; la información viaja cifrada

```bash
# Activar SSH y líneas virtuales
ip domain-name cisco
crypto key generate rsa
aaa new-model
ip ssh authentication-retries 3
ip ssh time-out 120
line vty 0 15
transport input ssh
exit
```

```bash
# Conectarse por SSH desde otra PC
ssh -l <usuario_admin> <IP_admin>
```

---

## Módulo 2 – Switching y Routing

### Modelo Jerárquico

Indica cómo debe estar implementada una red de switches a nivel empresarial. Consta de 3 capas:

| Capa | Función |
|------|---------|
| **Núcleo** | Lleva el tráfico al exterior |
| **Distribución** | Divide las cargas |
| **Acceso** | Conecta los dispositivos finales |

La conexión entre capas puede ser por **cable Ethernet cruzado** o **fibra óptica**.
Los switches se pueden fusionar para aumentar el número de puertos (por ejemplo, de 24 a 48).

#### Modelo Jerárquico de Núcleo Contraído

Existe: Núcleo, Trunk y Access; con Access para cada VLAN.

---

### VLANs (Virtual LAN)

- Pertenece a la **capa 2**
- Por cada VLAN hay un dominio de broadcast diferente
- Se crean en switches; por defecto existe la **VLAN 1**
- El archivo de VLANs se llama `vlan.dat`
- Número máximo: **4096**
  - Rango normal: 1 – 1005
  - Rango extendido: 1006 – 4096
- Mejoran la **seguridad** y **administración** de la red

> En **modo acceso**, un puerto permite tráfico de una sola VLAN.

```bash
# Ver VLANs creadas
do show vlan brief

# Crear VLANs
vlan <ID_VLAN>
name <NOMBRE_VLAN>
exit

# Asignar puertos a una VLAN (modo acceso)
interface fastEthernet 0/x
switchport mode access
switchport access vlan <ID_VLAN>
exit

# Asignar rango de puertos a una VLAN
interface range fastEthernet 0/x - y
switchport mode access
switchport access vlan <ID_VLAN>
exit

# Configurar puerto en modo trunk
interface fastEthernet 0/x
switchport mode trunk
switchport trunk allowed vlan <IDs_VLAN>
exit
```

---

### Trunk

- Usa el estándar **802.1Q**
- Permite el paso de una o más VLANs por el mismo enlace

---

### Enrutamiento entre VLANs (Router on a Stick)

```bash
# Subinterfaz por cada VLAN
interface gigabitEthernet 0/x/y.z
encapsulation dot1Q <ID_VLAN>
ip address <DIRECCIÓN_IP> <MÁSCARA>

interface gigabitEthernet 0/x/y.w
encapsulation dot1Q <ID_VLAN>
ip address <DIRECCIÓN_IP> <MÁSCARA>

# Habilitar la interfaz física
interface gigabitEthernet 0/x/y
no shutdown
```
