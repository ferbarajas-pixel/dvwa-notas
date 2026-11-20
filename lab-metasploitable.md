# Reconocimiento y explotación en Metasploitable 2
## Entorno del laboratorio
- Máquina atacante: Lubuntu (VM)
- Máquina víctima: Metasploitable 2 (VM)
- Red: Solo-anfitrión (Host-Only)
  
## nmap (escaneo)
- Comando: nmap ip |---| nmap -sV ip
- Resultado: En el primero obtuve los puertos mas comunes y ver cuales estaban abiertos y con el segundo vi las versiones de estos.

## FTP (vsftpd 2.3.4) - exploit
- Comando: searchsploit vsftpd 2.3.4 |---|  python3 /opt/exploitdb/exploits/unix/remote/49757.py ip (varia dependiendo de la ruta)
- Resultado: El primero es para saber en que ruta se encuentra el esa version que enocontramos como vulnerabilidad mediante el nmap anterior. 2. shell como root. El script automatiza enviar un usuario con ":)" al puerto 21, abriendo la puerta trasera en el puerto 6200.
## FTP Anonimo
-Comando: ftp ip
- Resultado: Conecta al servidor de archivos, probando "anonymous" como usuario y la contraseña vacía.

## SMB
- Comando: smbclient -L ip -N |---| smbclient //ip/tmp -N
- Resultado: "L" es las lista de carpetas compaertidas en red, "N" es pedir entrar sin contraseña entra sin autenticación y tiene permiso de escritura en /tmp.

## MySQL
- Comando: mysql -h ip -u root --ssl-mode=DISABLED 
- Resultado: "h" es poner el host, "u" es user o a que usuario entrar, en este caso el root sin contraseña. Se entro como el usuario root sin contraseña, usamos "SHOW DATABASES;" (importantes el ;) y ver otros datos.

## Banner Grabbing (SMTP y Telnet)
-Comando: nc -nv ip puerto (en estos casos 25 y 23) |---| nc -nv ip 80 | grep -i server
-Resultado: "nc" es netcat, "nv" es no buscar nombre de dominio, "|" una tuberia que manda la respuesta hacia grep, "-i" que ignore si la busqueda (en este caso server) este en mayusculas o minusculas. En el caso de HTTP al entrar ponemos: GET / HTTP/1.1 luego Host:IP + doble enter.

## 7. Telnet - login
- Comando: telnet ip
- Resultado: acceso con credenciales por defecto (msfadmin/msfadmin), terminal remota sin cifrado. Aquí se vio la diferencia entre esto, RDP y acceso remoto gráfico.



- Qué hice: 
- Resultado:
