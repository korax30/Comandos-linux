## Identificar puertos abeirtos
'''sh
nmap -sS -p- --open -min-rate 5000 -n -vvv -Pn -oG allPorts 
// -oG se guarda en formato grepeable para poder extraer los puertos con extractports // -sS escaneo sigiloso // -p- escanea todos los puertos --open // -min-rate 5000 Intenta enviar al menos 5000 paquetes por segundo // -n No realiza resolución DNS // -vvv Muestra resultados muy detallados // -Pn Desactiva la detección de hosts



