# Ejercicio CiberKillChain - Defensa


## Alumno

Eduardo Sciutto

## Enunciado

Desarrolla la defensa en función del ataque planteado en orden inverso



## Resolución

### Respuesta al ataque al nodo.

No queda otra opción que ir hasta el sitio y reconfigurarlo con el template correcto. Restablezco la frecuencia de reporte a 1 hora.
También procedo a cambiar la contraseña por default del usuario admin, y habilitar el usuario operador restringiendo su alcance sólo a visualizar los valores de las entradas digitales y analógicas y visualización de la configuración, sin permisos de edición.

### Respuesta al ataque al NS On Premise LoRaWAN

Primero procedo a aislar provisoriamente el servidor del NS de la red interna. Realizo investigaciones que incluyen pruebas forenses como verificar que data fue robada, credenciales utilizadas y evaluación de daños ocasionados. Necesito recopilar información que pueda utilizar como nueva línea de defensa en alguna de las etapas iniciales de la cadena de ataque.
El servidor debe conectarse a una subred segura de servidores. No debe ser accesible desde la red corporativa por cualquier usuario. Reviso la configuración de acceso en el firewall y dejo sólo permitidos los orígenes y puertos estrictamente necesarios. Reviso los usuarios con rol de administrador. Procedo a revisar el log de login y actividad. Intento detectar cual fue el usuario hackeado. Reestablezco igualmente todas las contraseñas. Implemento una nueva política de seguridad que obligue al cambio de contraseñas como mínimo cada 3 meses y mantengo actualizada la lista de administradores. Luego del análisis y evaluación del ataque, genero una acción en conjunto con el sector de seguridad informática para implementar a la brevedad un software adecuado para detección de anomalías y generación de alertas ante comportamientos fuera de lo común.

### Respuesta al ataque al ecosistema en Azure Cloud



Se plantea un ataque al sistema descripto siguiendo el modelo de 7 fases de la Kill Chain de la Ciberceguridad, mediante técnicas que se describen en las matrices de ATT&CK https://attack.mitre.org/matrices/.

En particular se analizaron técnicas para entornos Cloud Azure AD, Enterprise, SaaS y IaaS.

El atacante podría actuar sobre el nodo (dispositivo sensor LoRaWAN instalado en el AIB), pero tendría en el mejor de los casos un impacto aislado, acotado a la afectación de dicho dispositivo. En cambio, si logra vulnerar la seguridad de la gestión del servidor de red LoRaWAN (NS) o los componentes desplegados en Azure, que soportan la aplicación web y la base de datos, el impacto será mucho más significativo.

### Reconnaissance

#### Nodo:
- El yacimiento donde se instalan los nodos, es muy vasto y sólo tiene controles de personas en los caminos de acceso principales. No hay videovigilancia en cada AIB. Un intruso no identificado podría acceder a la ubicación del nodo, hacer un relevamiento exhaustivo de su Hw 


Se plantea un ataque al sistema descripto siguiendo el modelo de 7 fases de la Kill Chain de la Ciberceguridad, mediante técnicas que se describen en las matrices de ATT&CK https://attack.mitre.org/matrices/.

En particular se analizaron técnicas para entornos Cloud Azure AD, Enterprise, SaaS y IaaS.

El atacante podría actuar sobre el nodo (dispositivo sensor LoRaWAN instalado en el AIB), pero tendría en el mejor de los casos un impacto aislado, acotado a la afectación de dicho dispositivo. En cambio, si logra vulnerar la seguridad de la gestión del servidor de red LoRaWAN (NS) o los componentes desplegados en Azure, que soportan la aplicación web y la base de datos, el impacto será mucho más significativo.

### Reconnaissance

#### Nodo:
- El yacimiento donde se instalan los nodos, es muy vasto y sólo tiene controles de personas en los caminos de acceso principales. No hay videovigilancia en cada AIB. Un intruso no identificado podría acceder a la ubicación del nodo, hacer un relevamiento exhaustivo de su Hw e intentar conectarse por sus interfaces de configuración local (NFC o puerto USB). El software de gestion del nodo se descarga libremente de los Stores de Android e iOS. El firmware está protegido por una contraseña. Podría ocurrir que el instalador haya dejado la contraseña por default.

#### NS on Premise y Azure cloud 
- Aplicando técnicas de escaneo activo (por ejemplo wireshark, tcpdump) o aprovechando algún descuido de un empleado que gestione los servicios, el intruso podría obtener las credenciales de una cuenta de usuario de Azure o del NS on premise.  https://attack.mitre.org/techniques/T1595/ https://attack.mitre.org/techniques/T1078/ . 
También podría encontrarlas al estar guardadas de manera insegura. (Bash history, repositorios, archivos con información de acceso a sistemas, etc.) https://attack.mitre.org/techniques/T1552/

### Weaponization

#### Nodo: 
- El atacante planea y prepara una configuración del dispositivo adulterada.

#### NS on Premise y Azure cloud
- El atacante identifica una clave de acceso de un usuario de monitoreo y la URL del NS. Requiere acceso desde la red interna de la empresa.
- El atacante utiliza una cuenta de usuario y credenciales para acceder a una suscripción y grupo de recursos de Azure donde se despliegan los componentes de la solución. No hace falta tener acceso a la red interna de la compañía, ya que no hay ninguna restricción de acceso al cloud desde internet.

### Delivery

#### Nodo: 
- En una nueva visita al sitio, el atacante descarga la nueva configuración por NFC. Consulta los valores de lo sensores (sin mucho sentido ya que está en el lugar y ve el comportamiento del AIB).

#### NS on Premise y Azure cloud 
- Se despliega alguna herramienta de ransomware o spyware para seguir recabando información desde dentro.

### Explotación

#### NS on Premise y Azure cloud 
- El atacante modifica el proceso de autenticación, comprometiendo la confidencialidad de las credenciales o bypaseando algunos controles de acceso de sistemas utilizados en el cloud o en sistemas remotos (como ser VPNs y remote desktop)    https://attack.mitre.org/techniques/T1556/
- También eleva los privilegios del ambiente del dominio modificando la política vigente. (Por ejemplo en el IotHub con la política iothubowner) )https://attack.mitre.org/techniques/T1484/
- El atacante accede a los dashboards de servicios en el grupo de recursos de Azure para obtener información útil de un entorno operativo,  también ejecuta consultas adicionales y encuentra direcciones IP públicas y puertos abiertos para nuevos ataques. Esto permite que el adversario obtenga información sin realizar ninguna solicitud de API. https://attack.mitre.org/techniques/T1538/

### Instalation

#### NS on Premise y Azure cloud 
- Manipulación de cuenta. Sin afectar el acceso de la víctima, el atacante modifica roles y permisos de la cuenta para habilitar el movimiento lateral o tener mayores privilegios para llegar a su objetivo. https://attack.mitre.org/techniques/T1098/
- Se implementa algún servicio adicional que habilite el ingreso por otra vía por si por algún motivo es bloqueado el acceso ilegal utilizado.

### Command and Control

#### NS on Premise y Azure cloud
- Se usufructa la información recibida, como ser la base de datos https://attack.mitre.org/techniques/T1530/ . Permanentemente se inspecciona que la intrusión siga siendo no percibida, poniendo atención a las tareas de Auditoria de seguridad que tenga implementada la solución.

### Actions on Objectives

#### Nodo: 
- La nueva configuración desplegada en la visita al sitio, inutiliza al dispositivo. 
Otra acción puede ser modificar la frecuencia de reporting Interval a 1 vez por minuto, en vez de 1 vez por hora. Si esto se replicara a los “n” nodos de la red, afectará su performance.

#### NS on Premise y Azure cloud
- El intruso vende la información confidencial adquirida.
- El intruso realiza un ataque de endpoint o network Denial of Service (DoS) , para afectar la disponibilidad de los servicios a los usuarios. Por ejemplo saturando el ancho de banda con tráfico malicioso.  Por ejemplo usando un botnet y IP address spoofing para conducir el ataque (ZxShell, OnionDuke, Lucifer). https://attack.mitre.org/techniques/T1499/  https://attack.mitre.org/techniques/T1498/
- El intruso realiza un Account Access Removal  bloqueo/borrado de la cuenta (Por ejemplo LockerGoga) https://attack.mitre.org/techniques/T1531/
- El intruso realiza un borrado de datos. https://attack.mitre.org/techniques/T1485/ 
