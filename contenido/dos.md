# Configuración del Servidor

La instalación de Wazuh se puede realizar de forma completa en una maquina, o dividirlo por contenedores. En caso de usar menos de 100 clientes/agentes usaremos la instalación completa unica, si se va a monitorear mas de 100 clientes es recomendable realizar la instalación indicada en este [enlace.](https://documentation.wazuh.com/current/installation-guide/index.html)

Para realizar la instalación necesitamos una maquina con un sistema base de Ubuntu Server con los siguientes componentes:
- 8Gb de RAM minimo
- 25Gb disponibles en el disco duro
- IP Estatica
- Sistema Actualizado

En esta prueba voy a usar una Maquina Virtual en VirtualBox con las caracteristicas minimas indicadas anteriormente.

### 1.- Configurar MV/Server

![mv1](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas/mv1.png)
![mv2](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas/mv2.png)
![mv3](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas/mv3.png)

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
![ip_estatica](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas/ip_estatica.png)

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
![install1](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas/install1.png)
![install1](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas/install2.png)

Tras finalizar la instalación y configuración automatica, vamos al navegador e ingresamos con los datos que nos facilita en pantalla. Para acceder debemos *Mostrar los ajustes avanzados* y clickar en *Acceder a*.
![dash1](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas/dash1.png)

Aconsejo apuntar las credenciales en algun lugar seguro.
![dash2](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas/dash2.png)

Finalmente ya tenemos el Dashboard de Wazuh instalado.
![dash3](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas/dash3.png)

Vemos que no tenemos ningun cliente activo, por lo que vamos a pasar a instalar [clientes en Wazuh](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/contenido/tres.md)

:arrow_left: [VOLVER](https://github.com/kikeloppez/Wazuh-Monitoring)
