# Ejercicio CiberKillChain - Defensa


## Alumno

Eduardo Sciutto

## Enunciado

Desarrolla la defensa en función del ataque planteado en orden inverso. Considero dos escenarios de ataque. El primero al dispositivo IoT de campo (el nodo), el cual tiene un impacto acotado. El segundo a la infraestructura de servidor de red y a los servicios cloud de la solución, cuyo impacto de daño es mayor.



## Resolución

### Respuesta al ataque del nodo.

#### Actions on Objectives / Command and Control
No queda otra opción que ir hasta el sitio y reconfigurarlo con el template correcto. Restablezco la frecuencia de reporte a 1 hora.
#### Explotación
También procedo a cambiar la contraseña por default del usuario admin, y habilitar el usuario "operador" restringiendo su alcance sólo a visualizar los valores de las entradas digitales y analógicas y a la visualización de la configuración, sin permisos de modificación.
Preventivamente, aunque es muy improbable que fuese descubierta, se procede a la desafectación y creación de una nueva AppKey de LoRaWAN para el nodo y se realiza un rejoin a la red. De ésta manera dificulto cualquier intento de clonar un nodo en mi red.

### Respuesta al ataque del NS On Premise LoRaWAN

#### Actions on Objectives / Command and Control
Primero procedo a aislar provisoriamente el servidor del NS de la red interna.
#### Instalation
Realizo investigaciones que incluyen pruebas forenses como verificar que data fue robada, credenciales utilizadas y evaluación de daños ocasionados. Necesito recopilar información que pueda utilizar como nueva línea de defensa en alguna de las etapas iniciales de la cadena de ataque.
El servidor debe conectarse a una subred segura de servidores. No debe ser accesible desde la red corporativa por cualquier usuario.
#### Weaponization
Reviso la configuración de acceso en el firewall y dejo sólo permitidos los orígenes y puertos estrictamente necesarios.
#### Delivery
Reviso los usuarios con rol de administrador. Procedo a revisar el log de login y actividad. Intento detectar cual fue el usuario hackeado. Reestablezco igualmente todas las contraseñas.

Detecto el email malicioso con con la macro de randsomware. Identifico el usuario desprevenido que la ejecutó y desde alli busco reconstruir los pasos seguidos por el atacante. Uso de referencia la guía de Kaspersky de tacticas, técnicas y procedimientos para la defensa ante ataques de randsomware. (securelist.com/modern-randsomware-groups-ttps/106824)
#### Reconnaissance
Luego del análisis y evaluación del ataque, genero una acción en conjunto con el sector de seguridad informática para implementar a la brevedad un software adecuado para detección de anomalías y generación de alertas ante comportamientos fuera de lo común de los administradores.

Implemento una nueva política de seguridad que obligue al cambio de contraseñas como mínimo cada 3 meses y mantengo actualizada la lista de administradores.

### Respuesta al ataque al ecosistema en Azure Cloud

#### Actions on Objectives / Command and Control
Se accede mediante una cuenta de administrador principal (root access) y se bloquean todos los demás accesos. Se dejan fuera de servicio todos los componentes de la suscripción. Se revisa y audita la base de datos y se compara con copias de backup y ante la comprobación de estár corrupta se define levantarla desde un backup considerado seguro. La auditoría se hace extensiva a toda la gestión de la suscripción de las ultimas semanas, a fin de recabar toda la información posible sobre el ataque.

#### Instalation
Se crean nuevamente los usuarios y se reemplazan las credenciales de acceso.

#### Weaponization
Se revisa la configuración de todos los componentes en el grupo de recursos, en especial las políticas y roles para dejar ajustados los permisos de acceso a lo estrictamente necesario.

Se controla que se cumpla con las recomendaciones del estándar de seguridad para la gestión de identidades y acceso al entorno Cloud SAML 2.0 (Security Assertion Markup Language). En particular la correcta con figuración del Azure AD, la correcta gestión de las credenciales del usuario root (nadie lo debería usar) y la implementación de factor de doble autenticación para usuarios con funciones de mayores privilegios.


Se revisa documentación de Microsoft para implementar mejores barreras de protección en la nube https://learn.microsoft.com/en-us/azure/architecture/framework/security/monitor-tools 

Se define implementar el paquete Microsoft Defender for Cloud (en especial para Base de datos, Storage y App Service) a un costo aceptable para la solución https://azure.microsoft.com/es-es/pricing/details/defender-for-cloud/. Para tener un monitoreo continuo, recibir notificaciones de alerta y detectar amenazas de forma temprana. Esto por si solo no nos protege ya que se debe consensuar y aprobar un rol dentro de la empresa que tenga la responsabilidad de monitorear, actuar  y mantener al día ésta herramienta.

Para mitigar futuros intentos de ataque de DDoS desde internet, se evaluará la implementación de Azure DDoS Protection, que brinda protección a los recursos específicos de Azure en una red virtual. https://learn.microsoft.com/es-es/azure/ddos-protection/ddos-protection-reference-architectures

#### Reconnaissance
Se define reforzar la capacitación de los usuarios/administradores para tener un correcto manejo de actualizaciones del sistema y crear una conciencia en el uso de las redes y sus herramientas, para evitar ataques de ingeniería social.


