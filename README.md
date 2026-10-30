# Network Forensics
Análisis de tráfico de red usando Wireshark para identificar el acceso inicial, anular la ofuscación de un Javascript malicioso y extraer loe IOC's (ip, hashes de archivos, ejecución de procesos etc.)

---

Obtención de un pcap o parte de un log.

<img width="538" height="357" alt="image" src="https://github.com/user-attachments/assets/52604251-b59a-4c45-a6a1-d20330de9102" />

---


Escenario:

<img width="713" height="233" alt="image" src="https://github.com/user-attachments/assets/f38e7869-5400-467a-9ecf-3ad0e43b3cbd" />

---

Usaremos Kali sobre Proxmox como sistema operativo.


<img width="2520" height="1091" alt="image" src="https://github.com/user-attachments/assets/87db19ec-664a-461a-910c-00be74bd8a24" />

---

Para la obtención de credenciales usaremos KeepasXC.

<img width="801" height="645" alt="image" src="https://github.com/user-attachments/assets/0b2a9e06-f577-4c80-b25d-535f76f12d5c" />


---

Abrimos pcap con Wireshark

<img width="1076" height="746" alt="image" src="https://github.com/user-attachments/assets/0c634be6-a40a-4f0d-b583-b1ea17018915" />

Para la primera cuestión, con Wireshark es sencillo ver al usar el filtro http las conexiones que se establecen;

<img width="1111" height="255" alt="image" src="https://github.com/user-attachments/assets/15cdd995-1754-43ec-bb27-9a804524873e" />

<img width="2433" height="183" alt="image" src="https://github.com/user-attachments/assets/356c487b-1ef2-496e-b4e9-97c48f9a1c31" />

---

Para la segunda cuestión (Abajo), echamos un vistazo a ver si ha subido algo, o si ya hay algo en el servidor a qué llamar para establecer la conexión ;
http.request.method=="POST"

<img width="1111" height="255" alt="image" src="https://github.com/user-attachments/assets/40454a4e-2103-46ba-b54c-4d21529f9511" />
Que indica que no hay nada, a ver qué pasa con GET.

Echamos un vistazo al GET ;
http.request.method=="GET"

<img width="1991" height="194" alt="image" src="https://github.com/user-attachments/assets/14408faa-a384-4d36-b137-a9c822258127" />
Ahí lo tenemos, un javascript;  "allegato_708.js"

<img width="1375" height="504" alt="image" src="https://github.com/user-attachments/assets/3d9eac85-92c5-48cc-a4c1-cce96feccea9" />

Para la tercera pregunta, voy a coger las conexiones desde Wireshark, File, Export Objects, http y las guardo en el tmp en el que está el pcap.
<img width="1339" height="440" alt="image" src="https://github.com/user-attachments/assets/14ca2dba-337b-4097-88c7-3dabbe3f64f4" />
Teniendo esto ya podemos calcular el SHA256 u otro desde la terminal;

<img width="993" height="294" alt="image" src="https://github.com/user-attachments/assets/135e425c-e429-464e-96a2-86cca38bb4a0" />

La pregunta pide el sha256 de acceso inicial, con lo que es el del login, que echando un vistazo rápido a VirusTotal, en relaciones vemos los nombres que suele usar, y entre ellos el que hemos encontrado antes ;

<img width="1226" height="1109" alt="image" src="https://github.com/user-attachments/assets/636e869a-0d24-48ac-a455-18c02da19cf7" />

En la siguiente pregunta pide el proceso ejecutado, que ya tenemos en captura anterior en behavior de VirusTotal ;

<img width="1164" height="476" alt="image" src="https://github.com/user-attachments/assets/dc6d4c98-5497-4e19-b311-cdbb6dfdf9d6" />

La siguiente pregunta pide la extensión del segundo archivo malicioso. Esto lo tenemos en la captura cuando hemos exportado los objetos http o en la imagen del flow de GET más arriba, "resources.dll".

<img width="617" height="336" alt="image" src="https://github.com/user-attachments/assets/171662bf-7bcc-4a85-a657-e6722726031c" />

En la última pregunta, pide el MD5 de resources.dll, que tenemos en detalles de VirusTotal ;

<img width="1452" height="750" alt="image" src="https://github.com/user-attachments/assets/01f33151-51c8-4823-9ec7-493434b89508" />

Y con esto ya disponemos de toda la información relevante para enviar a la Dirección de empresa que determinará qué hacer legalmente etc.


<center><img width="600" height="1046" alt="image" src="https://github.com/user-attachments/assets/0026df0c-fd88-429f-973b-a43e68f06d47" /></center>

---





