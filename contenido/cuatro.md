# Envio de alertas mediante PostFix

En este paso vamos a configurar el servidor Wazuh para que funcione como Servidor de correo y pueda enviar una serie de alertas via email.

### 1.- Configuración de PostFix en Maquina Wazuh

Vamos a instalar una serie de paquetes que son necesarios para el funcionamiento del servidor de correo.
```
apt-get update && apt-get install postfix mailutils libsasl2-2 ca-certificates libsasl2-modules
```

Clickamos sobre *Sitio de Internet*.

![install1](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas3/install1.png)

Dejamos el nombre por defecto.

![install2](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas3/install2.png)

En caso de que nos pida reiniciar algun servicio, desmarcamos todos y avanzamos.

![install3](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas3/install3.png)

Ahora vamos a modificar el fichero de configuración de PostFix.
```
nano /etc/postfix/main.cf
```

Añadimos las siguientes lineas.
```
relayhost = [smtp.gmail.com]:587
smtp_sasl_auth_enable = yes
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_sasl_security_options = noanonymous
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt
smtp_use_tls = yes
smtpd_relay_restrictions = permit_mynetworks, permit_sasl_authenticated, defer_unauth_destination
```
En caso de querer enviar los correros a un servicio Outlook o diferente debemos cambiar la primera linea.
```
relayhost = [smtp.mail.outlook.com]:587
```
En mi caso vamos a seguir con Gmail.
![config1](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas3/config1.png)

**Importante revisar que ninguna linea se repita**

***En esta parte tenemos que usar una clave de aplicación que debemos configurar en Gmail, Outlook, y otros servicios***

Para encontrar la clave de aplicación en Gmail, debemos seguir los pasos del siguiente [enlace.](https://support.google.com/accounts/answer/185833?hl=es)
También puedes seguir el siguiente [video.](https://youtu.be/UoytTy1s47g)

Una vez la tenemos, la copiamos y la guardamos en algun lugar seguro.

Ejecutamos estos comandos con las credenciales.
```
echo [smtp.gmail.com]:587 email@gmail.com:CLAVE.DE.APP > /etc/postfix/sasl_passwd
postmap /etc/postfix/sasl_passwd
chmod 400 /etc/postfix/sasl_passwd
```
![config2](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas3/config2.png)

Ejecutamos los siguientes comandos.
```
chown root:root /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
chmod 0600 /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
```

Reiniciamos el servicio PostFix.
```
systemctl restart postfix
```

Realizamos una prueba de funcionamiento mediante el siguiente comando.
```
echo "Test mail from postfix" | mail -s "Test Postfix" -r "you@example.com" you@example.com
```

Comprobamos que han llegado los correros.
![prueba1](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas3/prueba1.png)
![prueba2](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas3/prueba2.png)

### 2.- Configuración del servicio Wazuh

Modificamos el siguiente fichero.
```
nano /var/ossec/etc/ossec.conf
```
El fichero se encuentra de la siguiente forma.

![config3](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas3/config3.png)

Modificamos las siguientes lineas.
```
<global>
  <email_notification>yes</email_notification>
  <smtp_server>localhost</smtp_server>
  <email_from>USERNAME@gmail.com</email_from>
  <email_to>you@example.com</email_to>
</global>
```

Quedaría de la siguiente forma.
![config4](https://github.com/kikeloppez/Wazuh-Monitoring/blob/main/galeria/capturas3/config4.png)

La linea marcada también podemos modificarla para indicar el numero de correos que se enviarán a la hora.

Finalmente, reiniciamos el servicio de Wazuh Manager.
```
systemctl restart wazuh-manager
```

:arrow_left: [VOLVER](https://github.com/kikeloppez/Wazuh-Monitoring)
