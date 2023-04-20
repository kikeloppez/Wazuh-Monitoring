# Envio de alertas mediante PostFix

En este paso vamos a configurar el servidor Wazuh para que funcione como Servidor de correo y pueda enviar una serie de alertas via email.

### 1.- Configuración del servidor

Vamos a instalar una serie de paquetes que son necesarios para el funcionamiento del servidor de correo.
```
apt-get update && apt-get install postfix mailutils libsasl2-2 ca-certificates libsasl2-modules
```

Clickamos sobre *Sitio de Internet*
![install1]()

Dejamos el nombre por defecto
![install2]()

En caso de que nos pida reiniciar algun servicio, desmarcamos todos y avanzamos.
![install3]()

Ahora vamos a modificar el fichero de configuración de PostFix
```
nano /etc/postfix/main.cf
```

Añadimos las siguientes lineas
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

:arrow_left: [VOLVER](https://github.com/kikeloppez/Wazuh-Monitoring)
