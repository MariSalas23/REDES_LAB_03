# Laboratorio III: Redes IPv6 en coexistencia con Redes IPv4

## Integrantes
- **Nicolás Almonacid Muñoz** (0000293190)
- **Juan Pablo Restrepo Coca** (0000305110)
- **Mariana Salas Gutiérrez** (0000296781)

## Video
Link (SharePoint)

## Introducción
La coexistencia de IPv4 e IPv6 en redes empresariales es fundamental para enfrentar los desafíos actuales de crecimiento de las redes y agotamiento de direcciones IPv4, es decir, IPv6 se ha vuelto importante para la escalabilidad y flexibilidad en las infraestructuras de red. Por ello, este informe explora el diseño, simulación y análisis de una red que permite la interoperabilidad entre ambos protocolos, utilizando Cisco Packet Tracer para la configuración y validación. Además, se destacan las problemáticas encontradas, así como las soluciones implementadas, y las conclusiones y recomendaciones a partir de los resultados del laboratorio.

## 1. Metodología
Para llevar a cabo el laboratorio y desarrollar la solución de la problemática establecida, se emplea la herramienta de **Cisco Packet Tracer** [1]. Este software nos permite diseñar y simular el comportamiento de una red empresarial, probando las configuraciones de routers, switches, servidores y otros dispositivos necesarios para el funcionamiento de la red. Se configuraron distintos protocolos esenciales como DNS, DHCP, SNMP y HTTP para asegurar el correcto funcionamiento de la red.
- **Montaje:** Inicialmente, se agregan al archivo de Packet Tracer: ocho computadores, seis switches (2811), un switch multicapa (3650), seis routers (2960), cuatro servidores y cuatro impresoras. Luego, se nombran los dispositivos como indica el documento. Después, se agrega el módulo WIC-2T para conexiones seriales en los routers. Posteriormente, se realiza la conexión por medio de las interfaces. Finalmente, se agregan las viñetas y recuadros para que quede más organizado.
- **Configuración:** La primera configuración que se realiza es la de los dispositivos switch para crear las VLAN y definir sus puertos. Posteriormente, se configuró R1_BOG y R2_ESP para asignar las direcciones IPv6 a las VLAN, usando DHCPv6 Stateful y SLAAC (Stateless Address Autoconfiguration), respectivamente. Los servidores cuentan con direcciones estáticas. Adicionalmente, a todos los routers y switches se les hizo la configuración básica (contraseña y hostname). Entonces, con esto se agregan los servicios de DNS y HTTP, junto con sus respectivos servidores, para poder acceder a una página web. El acceso a esta se limita con access lists. De manera similar, se incluye el protocolo SNMP para que solo pueda ser accedido desde dispositivos de la VLAN interna. Toda esta configuración se hace  en los routers R1_BOG y R2_ESP. Continuando con la red IPv4, las redes Intranet BOG e Intrnet MAD se conectan a través del internet mediante los routers con un túnel con IPsec VPN y dos protocolos de enrutamiento, OSPF (Open Shortest Path First) y EIGRP (Enhanced Interior Gateway Routing Protocol). Al final, se programa la aplicación Tracker utilizando su servidor y al PC4 como sistema de computo.
- **Verificación:** Primero, se envía un ping desde los routers R1_BOG y R2_ESP a los diferentes dispositivos para confirmar que estén bien conectados. Luego, se manda un ping desde PC1 a PC3 para verificar la conectividad entre la misma VLAN. De la misma manera, se revisa la conectividad entre VLAN diferentes. Después, se manda un ping entre routers y cuando funciona, se envía otro pero desde un PC. Posteriormente, se prueba la página como La última prueba que se realizó fue abrir la página *https://www.jnm.net* y *http://www.jnm.net* desde diferentes PC para evaluar el funcionamiento de las ACL. Igualmente, se hace con el SNMP cambiando el nombre de los routers R1_BOG y R2_ESP. La última verificación que se realiza es la aplicación Tracker con los PC4 y PC7.
- **Roles y Contribuciones:**
  * *Nicolás Almonacid (Relator - Programador - Presentador):* Realización de actas y exportación de configuraciones en archivos TXT - Configuración de la aplicación Tracker - Expositor en el video.
  * *Juan Pablo Restrepo (Encargado de redes - Presentador):* Montaje de la topología, configuración del túnel IPsec VPN y del enrutamiento (EIGRP y OSPF) -  Expositor en el video.
  * *Mariana Salas (Relatora - Encargada de redes - Presentadora):* Direccionamiento, realización de las tablas y creación de la Wiki - Configuración de VLANs y de los servicios/protocolos de DNS, HTTP, HTTPS, DHCPv6 Stateful, SLAAC, SNMP y ACL -  Expositora en el video. 

## 2. Resultados de configuración y verificación de funcionamiento de la topología

La topología representa dos redes IPv6 que se conectan mediante una red IPv4 (Internet). Estas dos son redes empresariales bajo el nombre de Intranet BOG e Intranet MAD. En el espacio DMZ están los servidores para el funionamiento de la página y de la aplicación.

![Imagen](https://github.com/MariSalas23/REDES_LAB_03/raw/main/lab3.png)
**Figura 1.** Topología.

### Elementos
- **Servidores:** Servidor DNS y servidor DHCP para la asignación de direcciones IP de manera dinámica.
- **Switches:** Se utilizaron switches 2960 para segmentar el tráfico en las redes locales.
- **Routers:** Cisco 2811, los cuales representan el internet y conectan las redes de Intranet BOG e Intranet MAD.
- **Dispositivos finales:** PCs e impresoras que se intercomunican entre ellos.

### Protocolos, servicios y modelos
- DNS (Sistema de nombres de dominio).
- DHCP (Protocolo de configuración dinámica de direcciones IP).
- HTTP (Hypertext Transfer Protocol).
- HTTPS (Hypertext Transfer Protocol Secure).
- SNMP (Simple Network Management Protocol).
- ACL (Access Control List).
- OSPF (Open Shortest Path First).
- EIGRP (Enhanced Interior Gateway Routing Protocol).
- Modelo TCP/IP.

### Segmentación mediante VLANs
Se crearon diferentes VLANs para Intranet BOG:
- **VLAN 101 (aa):** Para dispositivos invitados.
- **VLAN 102 (bb):** Para dispositivos internos.
- **VLAN 103 (cc):** Para el servidor e impresoras.
- **VLAN 999 (ee):** Nativa.

Se crearon diferentes VLANs para organizar Intranet MAD:
- **VLAN 101 (ff):** Para dispositivos invitados.
- **VLAN 102 (gg):** Para dispositivos internos.
- **VLAN 103 (hh):** Para el servidor e impresoras.
- **VLAN 999 (jj):** Nativa.

### Esquema de direccionamiento IPv4
Se aplicó una metodología de diseño estructurado, donde se segmenta la red en subredes adecuadas para garantizar la correcta distribución de direcciones IP. La segmentación asegura un manejo eficiente de los recursos de IP y la escalabilidad futura del sistema. Se emplea el servicio DHCPv6 Stateful y SLAAC con éxito como se ve a continuación.

![Imagen](https://github.com/MariSalas23/REDES_LAB_03/raw/main/DHCPv6.png)
**Figura 2.** DHCPv6 Stateful.


![Imagen](https://github.com/MariSalas23/REDES_LAB_03/raw/main/SLAAC.png)
**Figura 3.** SLAAC.

### SNMP
Para permitir la configuración remota, se utiliza SNMP. En la siguiente imagen se puede ver como logra realizar la operación "get" para obtener el nombre del router con éxito desde PC2 (dispositivo interno).

![Imagen](https://github.com/MariSalas23/REDES_LAB_03/raw/main/SNMP.png)
**Figura 4.** SNMP.

### Página Web
La visualización de la página personalizada también se logra como se muestra en la Figura 5. Para los PCs invitados (que pertenecen a la VLAN - Guest) se navega con *http://www.jnm.net*, mientras que los demás pueden acceder a ella con la url *https://www.jnm.net*. Lo anterior, se consigue gracias al uso de ACL.

![Imagen](https://github.com/MariSalas23/REDES_LAB_03/raw/main/pagina2.png)

**Figura 5.** Página web (HTTP y HTTPS).

### Listas de Acceso
Con el fin de que únicamente los PCs de la red interna deben gestionar sus respectivas Intranets (set y get) utilizando SNMP, al igual que permitir a los usuarios acceder a la página web alojada en el servidor Web a través del protocolo HTTPs (puerto 443) y no por HTTP (puerto 80), exceptuando los invitados, que acceden por el puerto 80, se emplean las ACL a continuación:

![Imagen](https://github.com/MariSalas23/REDES_LAB_03/raw/main/ACL.png)
**Figura 6.** Configuración de las ACL.

### Aplicación Tracker
...

![Imagen]()
**Figura 7.** Aplicación Tracker.

- Más capturas de configuración y verificación se encuentran en los siguientes apartados para resolver las preguntas propuestas en el laboratorio, analizar los resultados y justificar las conclusiones.

## 3. Respuestas a las preguntas formuladas en la sección de procedimiento

- **(1)**  El esquema de direccionamiento IPv4 basado en los requerimientos de red, y considerando X = 1, se presenta en las tablas de subnetting y direccionamiento en el apartado *4. Resultados y Análisis*.
  
- **(2)**  El montaje de la topología propuesta se puede visualizar en la *Figura 1*.
  
- **(3)**  Evalúe y configure los servicios de red IPv6 e IPV4 requeridos para la asignación eficiente del esquema de direccionamiento desarrollado. ¿Qué método(s) de asignación se debe(n) configurar? ¿En qué terminales se deben configurar los servicios requeridos?

- **(4)**  El Departamento de Tecnología le solicitó los siguientes filtros de paquetes: Todos los usuarios de la Intranet Bogotá acceden a la página web alojada en el servidor Web a través del protocolo HTTPs (puerto
443) y no por HTTP (puerto 80), exceptuando los usuarios invitados, que acceden por el puerto 80. Los usuarios invitados que ingresen a la Intranet Madrid deben tener restringido el acceso a la página web
por HTTPs (puerto 443) y acceder por HTTP (puerto 80). Finalmente, los usuarios de la empresa en la Intranet Madrid sólo deben acceder al servidor Web por el puerto 443. ¿Qué servicio de red se debe
configurar? La página web alojada en el Servidor Web debe ser personalizada. El nombre de dominio es gestionado por el servidor DNS. Este nombre debe tener el siguiente formato: Iniciales_nombres_estudiantes.net (e.g., jmalk.net)..

- **(5)**  Evalúe y configure los protocolos requeridos para la comunicación intra e inter VLANs y el protocolo de enrutamiento en las interfaces de red que se requieran. Hint. Enlace “Trunks”, IEEE 802.1q. ¿En qué interfaces se deben configurar OSPF o EIGRP (no RIP), OSPFv2 o EIGRPv6 (no RIPng), y redistribución entre protocolos? Analice los requerimientos de red.
  
- **(6)** Las intranets Bogotá y Madrid se interconectan de forma segura a través de INTERNET implementada completamente en IPv4. ¿Qué servicio(s) de migración se debe(n) implementar para permitir el acceso al servidor Web instalado en el DMZ configurado completamente en IPv6? ¿Qué servicios se deben configurar para tener una comunicación segura entre las Intranets? Evalúe y configure. Anexe evidencias
de la configuración realizada. Hint. Tunneling VPN con IPsec. ¿Dónde se deben configurar?

- **(7)** Soporte de gestión de red en ambas Intranet utilizando el estándar SNMP. Únicamente los PCs de la red interna deben gestionar sus respectivas Intranets (set y get) utilizando SNMP. Nota. ¿Qué servicio debe configurar para denegar el uso de SNMP a las demás VLANs?

- **(8)** No se utilizó otro servicio adicional.

- **(9)** Desarrolle una solución “Tracker” (software) orientada al seguimiento remoto de activos (PCs). El sistema computo, PC4, ubicado en la Intranet BOG, utiliza una aplicación “Tracker App” que se ejecuta internamente para monitorizar la temperatura y velocidad de reloj del procesador. Las mediciones de temperatura y velocidad de reloj son generadas aleatoriamente dentro de un rango de 30°C y 50°C, y 3.5 GHz y 4.0 GHz, respectivamente. Las mediciones capturadas por la “Tracker App” son enviadas al servidor “Tracker Server”, ubicado en el DMZ, cada segundo. El servidor “Tracker Server” cuenta con una aplicación “Tracker Replay” que recibe las mediciones enviadas por la “Tracker App” y las reenvía a la aplicación “Tracker Dashboard”. Ésta última se ejecuta en un computador, PC7, ubicado en la Intranet MAD. La aplicación “Tracker Dashboard” permite al técnico visualizar las mediciones capturadas por la aplicación
“Tracker App” y las alertas generadas al superar los 40°C y/o 3.5 GHz. Las aplicaciones intercambian mensajes a través de sockets. 

- **(10)** Los archivos TXT con las configuraciones también se encuentran anexados en la tarea de Teams.
     * [Configuración de Routers](https://github.com/MariSalas23/REDES_LAB_02/raw/main/Router_Config.txt)
     * [Configuración de Switches](https://github.com/MariSalas23/REDES_LAB_02/raw/main/Switch_Config.txt)

## 4. Resultados y Análisis

### 1) Responda cada pregunta guía del diseño estructurado propuesta en clase y documente todo el proceso de desarrollo del esquema de direccionamiento IPv4 propuesto por su equipo y diligencie las tablas de Subneteo y direccionamiento de la red empresarial.

#### Preguntas

**INTRANET BOGOTÁ**
- **¿Cuántas subredes necesito?** 2001:1200:A11:: / 48 necesita 4 subredes para la topología propuesta.
- **¿Cuántos hosts requieren?** No se especifica un número necesario de host en la guía de laboratorio. Sin embargo, es recomendado usar la mascara / 64 en la mayoría de las redes.
- **¿Qué dispositivos son parte de cada subnet?**
     * *VLAN 101 (aa):* Para PC1 y PC3 (Invitados).
     * *VLAN 102 (bb):* Para PC2 y PC4 (Interno).
     * *VLAN 103 (cc):* Para Servers y Printers.
     * *VLAN 999 (ee):* Para nodos intermedios.
- **¿Cuáles son privadas y públicas?** En IPv6, los dispositivos que necesitan acceso a Internet deben utilizar Global Unicast Addresses (GUAs). Los dispositivos que no necesitan conectarse a Internet pueden usar Unique Local Addresses (ULAs), que son direcciones privadas en IPv6.
- **¿Dónde deberían conservarse las direcciones?** Las direcciones son estáticas en los servidores. Las demás pueden ser dinámicas.
- **¿Cómo se asignan los dispositivos y las interfaces?** Se muestra en las tablas a continuación.

**INTRANET MADRID**
- **¿Cuántas subredes necesito?** 001:1200:B21:: / 48 necesita 4 subredes para la topología propuesta.
- **¿Cuántos hosts requieren?** No se especifica un número necesario de host en la guía de laboratorio. Sin embargo, es recomendado usar la mascara / 64 en la mayoría de las redes.
- **¿Qué dispositivos son parte de cada subnet?**
     * *VLAN 101 (ff):* Para PC5 y PC8 (Invitados).
     * *VLAN 102 (gg):* Para PC6 y PC7 (Interno).
     * *VLAN 103 (hh):* Para Servers y Printers.
     * *VLAN 999 (jj):* Para nodos intermedios.
- **¿Cuáles son privadas y públicas?** En IPv6, los dispositivos que necesitan acceso a Internet deben utilizar Global Unicast Addresses (GUAs). Los dispositivos que no necesitan conectarse a Internet pueden usar Unique Local Addresses (ULAs), que son direcciones privadas en IPv6.
- **¿Dónde deberían conservarse las direcciones?** Las direcciones son estáticas en los servidores. Las demás pueden ser dinámicas.
- **¿Cómo se asignan los dispositivos y las interfaces?** Se muestra en las tablas a continuación.

#### Tabla de Subnetting
![Imagen](https://github.com/MariSalas23/REDES_LAB_03/raw/main/lab31.png)

##### Proceso
Para calcular la dirección de broadcast de una red, identificamos la dirección IP y su máscara de subred. Ambas se convierten a binario, luego se realiza una operación AND entre la dirección IP y la máscara para obtener la dirección de red. Con esta dirección, se localizan los bits de host (ceros en la máscara) y se cambian todos esos bits por 1 en la dirección de red para obtener la dirección de broadcast. Por ejemplo, para la red 172.17.40.0/22, la dirección de broadcast resultante sería 172.17.43.255.

#### Tabla de Direccionamiento
![Imagen](https://github.com/MariSalas23/REDES_LAB_03/raw/main/lab32.png)

### 2) Describa el proceso de montaje, configuración y validación de los protocolos y servicios de red requeridos para el correcto funcionamiento de la topología de red. 

#### DNS
Respecto al proceso de configuración del DNS, primero se le asigna de forma estática su IP, es 161.130.2.4, la cual es la que se pone para configurar el DNS server en los dispositivos con el DHCP. Como se muestra en la siguiente imagen, el servicio de DHCP define el dominio como  *www.jnm.net* y lo dirige a 161.130.2.5, número que hace referencia al Web Server al ser su IP. Esto es lo que permite modificar el HTML y darle personalización a la página web.

![Imagen]()
**Figura 13.** Servidor DNS.

#### HTTP
Para configurar el servicio de HTTP primero se configuró la dirección IP de forma estática, de acuerdo con la tabla de direccionamiento. Como pertenece a la red de SERVERS, su dirección es 161.130.2.5, perteneciendo a la red 161.132.130.0 / 28. La máscara fue seleccionada para permitir 10 host, como indicaba el laboratorio. Finalmente, se modifica el index.html para que muestre la página personalizada que aparece en la *Figura 2*.

![Imagen]()
**Figura 14.** HTTP.

Los servicios DNS y HTTP demuestran ser exitosos y tienen el comportamiento esperado. Lo anterior se debe a que existe la debida conexión entre el servidor web y el servidor DNS, como se evidencia en la simulación. Además, se logra visualizar la página web como se ve en la *Figura 2* al ingresar, desde un PC por medio del web browser, *www.jnm.net*, que es la dirección creada a partir de las iniciales de los integrantes.

![Imagen]()
**Figura 15.** Conexión entre DNS y HTTP.

#### DHCPv6 Sateful
Continuando con el DHCP, se configura de manera estática su dirección IP, la cual pertenece a la red SOHO. Cada VLAN tiene su propio default gateway y dirección IP de inicio (con su respectiva máscara delimitada en la tabla), aunque comparten DNS Server (161.130.2.4) y WLC  (172.17.55.5). Todo esto se puede ver en la *Figura 3*, que aparece al inicio de la wiki. Finalmente, en R_SOHO se asignó como IP helper la dirección 172.17.55.2, haciendo referencia al servidor DHCP. La configuración del servicio se puede evidenciar con la conexión entre el servidor de DHCP y los diferentes dispositivos. 

![Imagen]()
**Figura 16.** Conexión entre Servidor DHCP y dispositivos.

La *Figura 3* también muestra una captura de cómo se le asigna al PC su dirección IP por medio del DHCP con éxito, demostrando una buena conexión, tanto a nivel físico como lógico, entre los dispositivos. Es decir, con una correcta comunicación gracias a las VLANs, su configuración en los diferentes switches, y buen manejo del R_SOHO.

#### SLAAC

#### SNMP

#### Aplicación Tracker

#### Enrutamiento

### 3) Evalúe el flujo bidireccional de datos generado por la solución de seguimiento remoto de paciente desde la aplicación “Tracker App”, pasando por la “Tracker Replay” y finalizando, en la aplicación “Tracker Dashboard”. Justifique su análisis utilizando capturas con el simulador y los filtros de paquetes de Cisco Packet Tracer.

...

### 4) Explique el flujo bidireccional de mensajes SNMP intercambiados entre los dispositivos gestionados desde las diferentes Intranets al utilizar capacidades “get” y “set” sobre una variable MIB de su elección. Justifique su análisis utilizando capturas con el simulador y los filtros de paquetes de Cisco Packet Tracer.

...

## 5. Retos presentados durante el desarrollo de la práctica
Durante el proceso de configuración en **Cisco Packet Tracer**, uno de los desafíos más grandes fue establecer la correcta comunicación entre los routers y las . Por ello, se realizó una búsqueda de información y se utilizó la fuente [2] para resolver dudas y seguir los pasos para implementar el túnel PIsec VPN. Igualmente, se presentaban problemas en la capa 3 en el enrutamiento, pero se solucionó creando rutas estáticas. La configuración del WLC también fue un gran reto, que al final no se pudo solucionar, ya que, aunque se ingresaba a la página resultante de la IP del WLC desde el web browser del PC, la configuración no se guardaba correctamente y no permitía avanzar al siguiente paso de abrir https://WLC_IP. El proceso descrito en [3] se intentó en los computadores de los tres integrantes del grupo. De acuerdo con la simulación, existe conectividad entre el PC1, el WLC y el LAP, indicando funcionamiento de la capa física y de la capa de enlace, por lo que el problema puede estar relacionado directamente con la configuración del WLC y no con las conexiones realizadas en la red por medio de los switches.

## 6. Conclusiones y Recomendaciones
En conclusión, la propuesta de la red empresarial permite la correcta conexión de una red de área local al internet. Durante el desarrollo de la solución se presentaron desafíos, especialmente en la implementación de VLANs y servicios como DHCP. A pesar de los retos, este trabajo reforzó los conocimientos del grupo sobre el diseño de redes empresariales y la configuración de dispositivos en **Cisco Packet Tracer**, logrando a través de la configuración de VLANs, DHCP, DNS y HTTP, establecer una red funcional que facilita la comunicación entre dispositivos. 

Se recomienda trabajar utilizando comandos como *show interfaces*, *show vlan brief*, *show running-config*, *show spanning-tree*, *show ip interface brief* y demás para lograr identificar problemas en las capas 1, 2 y/o 3. Adicionalmente, en Cisco Packet Tracer a veces es necesario reiniciar dispositivos cuando no están funcionando pese a que las configuraciones están bien hechas, ya que se trata de un entorno que puede presentar fallos temporales.

## 7. Referencias
[1] "Cisco Packet Tracer", *Cisco Systems*, 2024. [Enlace]. Disponible: https://www.netacad.com/courses/networking/

[2] "Configuración de TUNNEL GRE IPV6 Sobre IPV4 en Packet tracer 7.2.2", YouTube, 2020. [Online]. Disponible: https://www.youtube.com/watch?v=474pi7GAD-o. [Accessed: 12-Nov-2024].

[3] "Como Configurar un WLC y Servidor DHCP", YouTube, 2023. [Online]. Disponible: https://www.youtube.com/watch?v=WRF9f2hPIRA. [Accessed: 28-Sep-2024]. APP
