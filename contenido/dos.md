# Configuración del Servidor

La instalación de Wazuh se puede realizar de forma completa en una maquina, o dividirlo por contenedores. En caso de usar menos de 100 clientes/agentes usaremos la instalación completa unica, si se va a monitorear mas de 100 clientes es recomendable realizar la instalación indicada en este [enlace.](https://documentation.wazuh.com/current/installation-guide/index.html)

Para realizar la instalación necesitamos una maquina con un sistema base de Ubuntu Server con los siguientes componentes:
- 8Gb de RAM minimo
- 25Gb disponibles en el disco duro
- IP Estatica
- Sistema Actualizado

En esta prueba voy a usar una Maquina Virtual en VirtualBox con las caracteristicas minimas indicadas anteriormente.

### 1.- Configurar MV/Server

![mv1]()
![mv2]()
![mv3]()

Una vez logueado como usuario administrador o sudo su, debemos asegurarnos que el sistema está actualizado y tiene IP estatica.

Para comprobar que nuestro sistema está actualizado debemos usar los siguientes comandos:
```
apt update && apt upgrade
```

Para configurar la IP, lo mas óptimo es ver la dirección que nos ha establecido el servidor DHCP y configurarla para dejarla estatica. Usando el siguiente comando podemos ver la IP que tenemos.
```
ip a
```

Ahora nos vamos al fichero de configuración de red y establecemos las propiedades:
```
nano /etc/netplan/00-installer-config.yaml
```
![ip_estatica]()

Para aplicar la configuración usamos
```
netplan apply
```

### 2.- Instalación de Wazuh

Primeramente comprobamos que tengamos instalados los paquetes *curl* y *gpg*
```
apt install curl gpg -y
```
Ejecutamos el siguiente comando para instalar el paquete Wazuh
```
curl -sO https://packages.wazuh.com/4.4/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```

:arrow_left: [VOLVER](https://github.com/kikeloppez/Wazuh-Monitoring)
