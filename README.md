# Examen Redes


## 1. El Mural de las Siete Capas

El mural representa el Modelo OSI (Open Systems Interconnection), una representación conceptual del proceso de comunicación de datos en redes modernas. Cada capa se encarga de una función específica dentro del proceso de transmisión de datos:

1. Capa Física: Transmite los bits a través del medio físico (cables, señales eléctricas).
2. Capa de Enlace de Datos: Establece una conexión libre de errores entre dos dispositivos conectados directamente.
3. Capa de Red: Determina la mejor ruta para los datos (ej. IP).
4. Capa de Transporte: Garantiza la entrega de los datos completos y en orden (ej. TCP, UDP).
5. Capa de Sesión: Establece, mantiene y finaliza sesiones entre aplicaciones.
6. Capa de Presentación: Traduce datos entre formatos (ej. cifrado, compresión).
7. Capa de Aplicación: Punto de interacción con el usuario (ej. HTTP, FTP).

Este modelo ayuda a estructurar las funciones de red y entender cómo se produce la comunicación de extremo a extremo.

## 2. Los Dos Pergaminos del Mensajero

Los dos rituales representan los protocolos TCP (mensajero confiable) y UDP (mensajero veloz).

TCP (Transmission Control Protocol):
- Establece una conexión previa (handshake de tres pasos).
- Asegura la entrega de los datos y verifica errores.
- Ventaja: Fiabilidad.
- Desventaja: Mayor sobrecarga y lentitud.

UDP (User Datagram Protocol):
- No establece conexión previa.
- No garantiza la entrega ni el orden.
- Ventaja: Mayor velocidad y menor sobrecarga.
- Desventaja: Posibilidad de pérdida de datos.

Cada protocolo es útil dependiendo de la aplicación: TCP para correos o web, UDP para streaming o videojuegos.

## 3. El Enigma de las Subredes

La dirección base es 192.168.50.0 y se requieren 4 subredes iguales.
- Para obtener 4 subredes, se deben tomar 2 bits prestados del host (2^2 = 4).
- La máscara resultante será: 255.255.255.192 o /26.
- Cada subred tendrá 64 direcciones, de las cuales 62 son utilizables (se restan la red y el broadcast).

Subredes:
- 192.168.50.0/26 (hosts: 192.168.50.1–62)
- 192.168.50.64/26 (hosts: 192.168.50.65–126)
- 192.168.50.128/26 (hosts: 192.168.50.129–190)
- 192.168.50.192/26 (hosts: 192.168.50.193–254)

Así los cuatro gremios pueden coexistir con sus propios rangos.

## 4. La Encrucijada de las Rutas

El tótem representa una tabla de enrutamiento. Esta tabla guía a los routers en la toma de decisiones sobre por dónde enviar los paquetes de datos.

- Las flechas talladas representan rutas estáticas: fijas, configuradas manualmente.
- Las flechas móviles representan rutas dinámicas: aprendidas y modificadas automáticamente por protocolos como RIP, OSPF o EIGRP.

Una tabla de enrutamiento contiene:
- Redes de destino
- Máscaras de red
- Puertas de enlace (gateways)
- Interfaces de salida
- Métricas de preferencia

El router consulta esta tabla para dirigir cada paquete al siguiente salto adecuado.

## 5. El Guardián de la Máscara Única

Esta metáfora representa la técnica de NAT (Network Address Translation), concretamente PAT (Port Address Translation).

- En una red privada, múltiples dispositivos pueden compartir una sola dirección IP pública.
- Al salir, el router cambia la dirección IP del emisor por la suya y guarda el puerto de origen.
- Cuando la respuesta llega, sabe a qué dispositivo reenviar gracias a la tabla de traducción.

Beneficios:
1. Seguridad: oculta la red interna del mundo exterior.
2. Conservación de direcciones IPv4 públicas.

Así, múltiples 'rostros' internos usan una sola 'máscara' para salir al exterior sin revelar su identidad.






# Crónica Técnica del Gran Enlace: Las Dos Ciudades

> *"En un vasto mundo digital, dos civilizaciones separadas por un árido desierto binario decidieron tender un puente de luz entre sus reinos, guiadas por las antiguas escrituras de los protocolos y protegidas por los guardianes de fuego."*

---

## Fundación de las Ciudades

Las dos urbes, **Ciudad A** y **Ciudad B**, fueron edificadas en simetría perfecta. Cada una, rodeada por tres zonas místicas: el **Interior**, la **DMZ** y el **Exterior**, fue tallada en silicio para proteger y guiar la transmisión de conocimiento y servicios.

En el centro de cada ciudad se alza una poderosa fortaleza: el **ASA Firewall**. Estos guardianes fueron invocados con interfaces sagradas:

- `GigabitEthernet1/1` – outside (zona exterior)
- `GigabitEthernet1/2` – dmz (zona desmilitarizada)
- `GigabitEthernet1/3` – inside (zona interna)

Ambos ASA, rebautizados como **CiudadA** y **CiudadB**, establecen las reglas de paso entre los mundos internos, los caminos comerciales de la DMZ y los oscuros rincones del desierto exterior.

---

## El Desierto de los 200.0.0.x – El Gran Vacío

Entre ambas civilizaciones se extiende el **Desierto de Frame-Relay**, identificado con las coordenadas **200.0.0.0/30**. A través de esta vasta zona se comunican los **Router0** y **Router1**, con enlaces seriales point-to-point, guiados por los DLCIs 102 y 201.

Sus rutas fueron cinceladas con sumo cuidado para que cada uno reconociera los caminos hacia las redes lejanas.

---

## Los Guardianes de Fuego: ASA Configurados

Ambos ASA fueron invocados con los mismos rituales, aunque adaptados a los rangos de sus dominios. Se levantaron con:

- Objetos NAT para las zonas inside y dmz  
- ACL únicas `ALL_ICMP` para permitir visibilidad durante la gran prueba de conectividad.
- Rutas estáticas hacia todos los reinos vecinos, para no perderse en el viaje digital.

Cada uno defendía tres subredes:

| Zona        | Ciudad A (ASA A)     | Ciudad B (ASA B)     |
|-------------|----------------------|----------------------|
| Inside      | 192.168.10.0/24      | 192.168.30.0/24      |
| DMZ         | 192.168.50.0/24      | 192.168.60.0/24      |
| Outside     | 192.168.20.0/24      | 192.168.40.0/24      |

---

## Los Routers Interiores: Oráculos de Red

Cada ciudad contaba con un router sabio, conectado al ASA desde el lado inside, que llevaba la voz del pueblo hacia el resto del mundo.

### Ciudad A – Router Interno
- Interfaz LAN: `192.168.10.1/24`
- Rutas hacia `192.168.20.0/24`, `192.168.50.0/24` y las rutas lejanas vía `192.168.20.2`

### Ciudad B – Router Interno
- Interfaz LAN: `192.168.30.1/24`
- Rutas hacia `192.168.40.0/24`, `192.168.60.0/24` y lo distante vía `192.168.40.2`

---

## Pruebas de Conectividad – El Viaje de los Paquetes

En las calles de cada ciudad, humildes aldeanos (PCs) enviaron señales hacia el más allá. Gracias a las rutas grabadas y los hechizos NAT, los paquetes comenzaron a atravesar:

- Desde PC-A (192.168.10.10) hasta PC-B (192.168.30.10)  
- Desde DMZ de A hasta DMZ de B  
- Desde la tierra de los servidores al exterior del desierto

Cada prueba fue superada con éxito tras muchas tormentas (errores de ACL, NAT duplicados, rutas ausentes).

---

## Seguridad y Visión

Las reglas fueron escritas con claridad:

- NAT dinámico para inside y dmz → outside
- ACL únicas en cada ASA para permitir ICMP
- Rutas completas para alcanzar todos los subreinos

Y el fuego de los ASA no dejó pasar nada que no estuviera permitido explícitamente. Las tablas `xlate` y `access-list` fueron consultadas como oráculos.

---

## Servicios en la Tierra de la DMZ

En ambas ciudades se alzaron templos servidores:

- HTTP/HTTPS – Servidores web
- FTP – Transferencia de archivos sagrados
- MAIL – Envío de mensajes divinos vía SMTP y POP3

Cada uno con su propia IP estática y escuchando desde la zona DMZ. Los accesos desde el exterior fueron permitidos con ACL específicas hacia sus puertos.

---


![dsfs](https://github.com/user-attachments/assets/faadf3f5-91eb-4a46-a2a5-8102ee603864)






# EJ2. Crónicas de las Dos Ciudades Conectadas – Implementación Técnica de Red


En este proyecto se implementa una red jerárquica dividida en dos ciudades interconectadas por un enlace punto a punto. Cada ciudad contiene una topología de red estructurada con switches de acceso, un switch de distribución (central) y un router configurado con subinterfaces (`router-on-a-stick`) para enrutamiento entre VLANs.

## Topología General

- **Ciudad Este (Router1)**
  - VLAN 10: Arquitectos – 192.168.10.0/24
  - VLAN 20: Escribas – 192.168.20.0/24
  - VLAN 30: Mensajeros – 192.168.30.0/24

- **Ciudad Oeste (Router2)**
  - VLAN 40: Ingenieros – 192.168.40.0/24
  - VLAN 50: Diseñadores – 192.168.50.0/24

- **Enlace WAN entre ciudades:** 10.0.0.0/30 (Gi0/0/1 entre ambos routers)

## Configuración de VLANs y Trunking

Cada ciudad contiene tres switches de acceso, uno por VLAN, conectados mediante enlaces `trunk` a un switch central. Este switch central también se conecta al router correspondiente usando un enlace trunk.

- Los puertos entre los switches de acceso y el switch central están en modo `trunk`.
- En cada switch de acceso, los puertos hacia PCs están en modo `access` y asignados a su VLAN.

## Configuración de Routers

En cada router se crean subinterfaces para cada VLAN con `encapsulation dot1Q` y se asigna la dirección IP de gateway de la subred.

### Ejemplo (Router1):

```
interface gig0/0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
interface gig0/0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
interface gig0/0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0
interface gig0/0/1
 ip address 10.0.0.1 255.255.255.252
```

### Rutas Estáticas

Ambos routers usan rutas estáticas para alcanzar las VLANs del otro lado.

**Router1:**
```
ip route 192.168.40.0 255.255.255.0 10.0.0.2
ip route 192.168.50.0 255.255.255.0 10.0.0.2
```

**Router2:**
```
ip route 192.168.10.0 255.255.255.0 10.0.0.1
ip route 192.168.20.0 255.255.255.0 10.0.0.1
ip route 192.168.30.0 255.255.255.0 10.0.0.1
```

## Direccionamiento IP Estático

No se utilizó DHCP. Cada PC fue configurada manualmente con dirección IP y gateway correspondientes a su VLAN.

## Verificación

Se verificó conectividad mediante `ping`:
- Entre PCs de la misma VLAN (intra-VLAN)
- Entre PCs de distintas VLANs dentro de la misma ciudad (inter-VLAN routing)
- Entre PCs de distintas ciudades (enlace WAN + rutas estáticas)

## Conclusión

Este proyecto demuestra el diseño e implementación de una red segmentada con VLANs, enrutamiento inter-VLAN mediante subinterfaces y enlace entre dos dominios de red mediante rutas estáticas. La solución es jerárquica, escalable y refleja un modelo realista de red empresarial distribuida.



![EJ2](https://github.com/user-attachments/assets/fe09fd98-24d3-463a-b7af-7f0dfcfcbfbe)
