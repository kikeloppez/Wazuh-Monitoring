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

Aplicamos la configuración con el siguiente comando.
```
systemctl restart networking.service
```

### 2.- Instalación del paquete Wazuh Agent.

En primer lugar ejecutamos el siguiente comando para instalar los paquetes *curl* y *gpg*
```
apt install curl gpg -y
```
Ejecutamos el siguiente comando.
```
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg
```
![clave]()

Añadimos repositorios.
```
echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list
```
![repos]()



:arrow_left: [VOLVER](https://github.com/kikeloppez/Wazuh-Monitoring)
