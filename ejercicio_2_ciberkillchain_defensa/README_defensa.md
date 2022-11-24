# Ejercicio CiberKillChain - Defensa


## Alumno

Eduardo Sciutto

## Enunciado

Desarrolla la defensa en función del ataque planteado en orden inverso



## Resolución

### Respuesta al ataque del nodo.

No queda otra opción que ir hasta el sitio y reconfigurarlo con el template correcto. Restablezco la frecuencia de reporte a 1 hora.
También procedo a cambiar la contraseña por default del usuario admin, y habilitar el usuario operador restringiendo su alcance sólo a visualizar los valores de las entradas digitales y analógicas y visualización de la configuración, sin permisos de edición.

### Respuesta al ataque del NS On Premise LoRaWAN

Primero procedo a aislar provisoriamente el servidor del NS de la red interna. 
Realizo investigaciones que incluyen pruebas forenses como verificar que data fue robada, credenciales utilizadas y evaluación de daños ocasionados. Necesito recopilar información que pueda utilizar como nueva línea de defensa en alguna de las etapas iniciales de la cadena de ataque.
El servidor debe conectarse a una subred segura de servidores. No debe ser accesible desde la red corporativa por cualquier usuario. 
Reviso la configuración de acceso en el firewall y dejo sólo permitidos los orígenes y puertos estrictamente necesarios. 
Reviso los usuarios con rol de administrador. Procedo a revisar el log de login y actividad. Intento detectar cual fue el usuario hackeado. Reestablezco igualmente todas las contraseñas.
Implemento una nueva política de seguridad que obligue al cambio de contraseñas como mínimo cada 3 meses y mantengo actualizada la lista de administradores. 
Luego del análisis y evaluación del ataque, genero una acción en conjunto con el sector de seguridad informática para implementar a la brevedad un software adecuado para detección de anomalías y generación de alertas ante comportamientos fuera de lo común.

### Respuesta al ataque al ecosistema en Azure Cloud



