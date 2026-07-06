# danabot (Network Forensics)
Analyze network traffic using Wireshark to identify DanaBot initial access, deobfuscate malicious JavaScript, and extract IOCs like IPs, file hashes, and execution processes.

Obtención de un pcap.
<img width="538" height="357" alt="image" src="https://github.com/user-attachments/assets/52604251-b59a-4c45-a6a1-d20330de9102" />

Escenario:

<img width="713" height="233" alt="image" src="https://github.com/user-attachments/assets/f38e7869-5400-467a-9ecf-3ad0e43b3cbd" />

Questiones a resolver:

<img width="857" height="1172" alt="image" src="https://github.com/user-attachments/assets/74b434a0-4ed9-4b91-88dd-102c37aa22b9" />

Como siempre Kali, aunque esta vez desde Oracle VirtualBox, porque Proxmox tiene pendiente una mejora de procesador.

<img width="657" height="503" alt="image" src="https://github.com/user-attachments/assets/39eb5f36-7422-4646-9fab-5569c8ba707a" />


Abrimos pcap con Wireshark

<img width="1076" height="746" alt="image" src="https://github.com/user-attachments/assets/0c634be6-a40a-4f0d-b583-b1ea17018915" />

Para la primera cuestión, con Wireshark es sencillo ver al usar el filtro http las conexiones que se establecen;

<img width="1111" height="255" alt="image" src="https://github.com/user-attachments/assets/15cdd995-1754-43ec-bb27-9a804524873e" />

<img width="2433" height="183" alt="image" src="https://github.com/user-attachments/assets/356c487b-1ef2-496e-b4e9-97c48f9a1c31" />


Para la segunda cuestión, echamos un vistazo a ver si ha subido algo, o si ya hay algo en el servidor a qué llamar para establecer la conexión ;
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







