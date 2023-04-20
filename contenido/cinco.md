# Activar detección de vulnerabilidades

Para este paso debemos activar unas caracteristicas tanto en el cliente como en el servidor.

Este paso es muy importante hacerlo el ultimo para que nuestro servidor PostFix esté activo cuando el escaner empiece a funcionar y envie por correo las vulnerabilidades de los equipos implantados al servidor.

### 1.- Activar caracteristica en Cliente/Agente

En primer lugar, vamos a añadir unas lineas al fichero de configuración del agente.
```
nano /var/ossec/etc/shared/agent.conf
```
```
<wodle name="syscollector">
   <disabled>no</disabled>
   <interval>1h</interval>
   <os>yes</os>
   <packages>yes</packages>
   <hotfixes>yes</hotfixes>
</wodle>
```
De forma que quede así.

![config1](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas4/config1.png)

### 2.- Activar caracteristica en Servidor/Manager

Modificamos el fichero de configuración del servidor
```
nano /var/ossec/etc/ossec.conf
```

Podemos comprobar que la sección *enabled* esta desactivada. Hay que cambiar el *no* por *yes*. Tambien hay que activar con *yes* todos los sistemas que queremos que escanee.

![config2](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas4/config2.png)

Tendría que quedar de la siguiente forma.

![config3](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas4/config3.png)

Finalmente reiniciamos el servicio y comprobamos.
```
systemctl restart wazuh-manager
```

:arrow_left: [VOLVER](https://github.com/kikeloppez/Wazuh-Monitoring)
