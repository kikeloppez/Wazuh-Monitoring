# Configuración del Servidor

La instalación de Wazuh se puede realizar de forma completa en una maquina, o dividirlo por contenedores. En caso de usar menos de 100 clientes/agentes usaremos la instalación completa unica, si se va a monitorear mas de 100 clientes es recomendable realizar la instalación indicada en este [enlace.](https://documentation.wazuh.com/current/installation-guide/index.html)

Para realizar la instalación necesitamos una maquina con un sistema base de Ubuntu Server con los siguientes componentes:
- 8Gb de RAM minimo
- 25Gb disponibles en el disco duro
- IP Estatica
- Sistema Actualizado

En esta prueba voy a usar una Maquina Virtual en VirtualBox con las caracteristicas minimas indicadas anteriormente.

### 1.- Configurar MV/Server

![1]()
![2]()

Una vez logueado como usuario administrador o sudo su, debemos establecer una IP estatica. Lo mas optimo es ver la IP que nos ha establecido el servidor DHCP y configurarla para dejarla estatica. Usando el siguiente comando podemos ver la IP que tenemos.
```
ip a
```

Ahora nos vamos al fichero de configuración:

```
nano /etc/netplan/00-installer-config.yaml
```

:arrow_left: [VOLVER](https://github.com/kikeloppez/Wazuh-Monitoring)
