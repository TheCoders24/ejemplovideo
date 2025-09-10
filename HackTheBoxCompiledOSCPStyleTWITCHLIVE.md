# HackTheBox | Compiled [OSCP Style]

<[text](https://www.youtube.com/watch?v=g8OA2O9Nbps&ab_channel=S4viOnLive%28BackupDirectosdeTwitch%29)>

## Escaneo de Puertos  usando NMAP

--> me va a reporta por consola todos lo puertos que esten abiertos  

***nmap -p-  --open -sS --min-rate 5000 -vvv -n -Pn <IP> -oG ollPorts***

--> le lanzamos unos script de reconocimientos para podersaber con lo que nos estamos enfrentado y lo guardamos en un archivo Targeted

***nmap -p3000,5000,5985 -sC -sV -oN targeted <IP>***

--> con la herramienta whatweb tratamos de identificar que servicios estan corriendo sobre la pagina web que exite y podriamos saber con lo que nos estamos enfrentado
--> investigamos accediendo a la web si es que esta disponible

***whatweb <IP>:Ports***

--> nos ponemos en escucha por el puerto 80  para ver que tipo de peticiones esta haciendo y ver que podemos obtener

***nc -nlvp 80***

-->se econtro que atravez de un git clone se puede ejecutar commandos y la version de el git