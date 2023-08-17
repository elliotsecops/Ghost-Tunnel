# Túnel SSH Anónimo sobre Tor 

Este proyecto implementa un poderoso túnel SSH totalmente anónimo utilizando la red Tor y múltiples proxies intermedios. Permite enrutar cualquier tráfico de red a través de este túnel de forma altamente privada y anónima.

## Características Principales

- **Rotación automática de servidores SSH intermediarios** - La conexión se establece cada vez a través de un servidor SSH diferente de una lista rotativa. Esto maximiza el anonimato al no utilizar el mismo servidor dos veces.

- **Obtención de nuevas identidades Tor** - Se obtienen periódicamente nuevas identidades y circuitos Tor para prevenir el rastreo de la dirección IP de salida. La IP de salida se rota constantemente.

- **Autenticación con proxies** - Soporta la autenticación con credenciales en los proxies SOCKS5 intermedios para permitir el uso de proxies privados.

- **Totalmente enrutado a través de SSH** - Todo el tráfico se enruta automáticamente a través del túnel SSH utilizando PySocks. No es necesaria ninguna configuración especial en las aplicaciones.

- **Funciona con cualquier aplicación** - Al enrutar el tráfico a nivel de sistema, cualquier aplicación que utilice sockets funcionará directamente a través del túnel SSH. No se requiere soporte explícito de proxies.

- **Scripts para rotar identidad y proxy** - Se incluyen scripts simples para obtener una nueva identidad Tor o proxy intermediario bajo demanda. Útil para rotar periodicamente.

## Requisitos Previos

Para utilizar este túnel SSH anónimo se requiere tener instalado:

- **Python 3** - El intérprete de Python 3.6 o superior.
- **Stem** - Biblioteca Python para interactuar con Tor.
- **PySocks** - Permite enrutar tráfico a través de proxies SOCKS.
- **Paramiko** - Módulo SSH para Python.

Además se debe tener:

- Acceso a servidores **SSH** que permitan tunneling (ej: en la nube).
- El servicio **Tor** corriendo y accesible en localhost:9050 (mediante Tor Browser Bundle o tor).
- Proxies **SOCKS5** compatibles con autenticación (opcional).

## Configuración

Antes de ejecutar el script se deben configurar los siguientes valores:

- `ssh_hosts` - Lista de servidores SSH intermediarios
- `ssh_user` - Usuario para conectar a los servidores SSH
- `ssh_password` - Contraseña asociada
- `proxies_user` - Usuario para autenticarse con los proxies
- `proxies_password` - Contraseña para los proxies

Un ejemplo de configuración sería:

```python
ssh_hosts = ['servidor1.com', 'servidor2.net']
ssh_user = 'tuneluser'
ssh_password = 'contraseñaSegura' 
proxies_user = 'proxiusuario'
proxies_password = 'secreta123'
```

## Uso

Una vez configurado, para iniciar el túnel SSH simplemente ejecutar el script Python:

```bash
python tunelssh.py
```

Esto establecerá el túnel a través de un servidor SSH intermediario elegido al azar y configurará el sistema para enrutar todo el tráfico a través de él.

Luego se puede verificar que el tráfico sale a través de Tor utilizando un servicio como [OnionCheck ↗](https://onioncheck.com/).

## Rotación de Identidad y Proxy

Para rotar la IP de salida de Tor se puede ejecutar el siguiente script:

```bash
python nueva_identidad.py
```

Esto forzará la obtención de un nuevo circuito y dirección IP de salida.

De forma similar, para cambiar el proxy SOCKS5 intermediario:

```bash
python nuevo_proxy.py
```

Se recomienda rotar periodicamente tanto la IP de Tor como el proxy para maximizar el anonimato.

## Contribuciones

Este proyecto es de código abierto, así que son bienvenidas las contribuciones vía pull requests:

- Mejoras de rendimiento y estabilidad.
- Soporte para otras plataformas.
- Compatibilidad con otras bibliotecas.
- Características de seguridad adicionales.

(English)

# Anonymous Tor SSH Tunnel

This project implements a powerful, fully anonymous SSH tunnel using the Tor network and multiple proxy servers. It allows routing any network traffic through this tunnel in a highly private and anonymous way.

## Main Features

- **Rotating SSH proxies** - The connection is established each time through a different SSH server from a rotating list. This maximizes anonymity by not using the same server twice.

- **Getting new Tor identities** - New Tor identities and circuits are periodically obtained to prevent tracking of the exit IP address. The exit IP rotates constantly.

- **Proxy authentication** - Supports credential-based authentication with SOCKS5 proxy servers to allow the use of private proxies.

- **Fully SSH-routed** - All traffic is automatically routed through the SSH tunnel using PySocks. No special configuration required in applications.

- **Works with any app** - By routing at the system level, any socket-using app will work directly through the SSH tunnel. No explicit proxy support needed.

- **Scripts for rotating** - Includes simple scripts to get a new Tor identity or proxy on demand. Useful for periodic rotation.

## Requirements

To use this anonymous SSH tunnel you need to have installed:

- **Python 3** - The Python 3.6 or later interpreter.
- **Stem** - Python library for interacting with Tor.
- **PySocks** - Allows routing traffic through SOCKS proxies.
- **Paramiko** - SSH module for Python.

Additionally required:

- Access to **SSH** servers allowing tunneling (e.g. in the cloud).
- The **Tor** service running and accessible on localhost:9050 (via Tor Browser Bundle or tor).
- **SOCKS5** proxies compatible with authentication (optional).

## Configuration

Before running the script, the following values must be configured:

- `ssh_hosts` - List of intermediate SSH servers
- `ssh_user` - Username for connecting to SSH servers
- `ssh_password` - Associated password
- `proxies_user` - Username for proxy authentication
- `proxies_password` - Password for proxies

A configuration example:

```python
ssh_hosts = ['server1.com', 'server2.net']
ssh_user = 'tunneluser' 
ssh_password = 'securePassword'
proxies_user = 'proxyuser'
proxies_password = 'secret123'
```

## Usage

Once configured, to start the SSH tunnel simply run the Python script:

```bash
python ssh_tunnel.py
```

This will establish the tunnel through a randomly chosen intermediate SSH server and configure the system to route all traffic through it.

You can then check that traffic is exiting through Tor using a service like [OnionCheck](https://onioncheck.com/).

## Identity and Proxy Rotation

To rotate the Tor exit IP, run the following script:

```bash
python new_identity.py
```

This will force a new circuit and exit IP address.

Similarly, to change the intermediate SOCKS5 proxy:

```bash
python new_proxy.py 
```

It's recommended to periodically rotate both the Tor IP and proxy for maximum anonymity.

## Contributing

This is an open source project, so contributions are welcome via pull requests:

- Performance and stability improvements.
- Support for other platforms.
- Compatibility with other libraries.
- Additional security features.
