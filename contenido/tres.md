# Configuración de los Clientes

Para poder monitorear los agentes, debemos instalar una serie de paquetes en el cliente que permite al Servidor poder leer todos los datos y mostrarlos en el dashboard como en los ejemplos vistos en la sección de [Galeria.](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/contenido/galeria.md)

Para esta prueba vamos a realizar la conexión con un cliente Debian 11, aunque la implementación de agentes está disponible para cualquier tipo de Sistema.

En caso de querer establecer la conexión con otro sistema, clicke en el siguiente [enlace](https://wazuh.com/install/) y desplacese hasta el final de la página, donde encontrarás todos los sistemas admitidos por Wazuh.

### 1.- Configuración del Cliente


En primer lugar vamos a acceder como superusuario y comprobar que el equipo esté actualizado, para ello usaremos el siguiente comando.
```
apt update && apt upgrade -y
```

También vamos a establecer una IP estatica. Para ello modificamos el siguiente fichero y añadimos las siguientes lineas.
```
nano /etc/network/interfaces
```
![ip_estatica]()

Aplicamos la configuración con el siguiente comando
```
systemctl restart networking.service
```

:arrow_left: [VOLVER](https://github.com/kikeloppez/Wazuh-Monitoring)
