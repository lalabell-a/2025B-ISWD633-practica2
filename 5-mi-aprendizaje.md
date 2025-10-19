# COMPLETAR  
Comparando sus conocimientos antes de hacer la práctica con sus conocimientos después de hacer la tarea, explicar los principales aprendizajes logrados para beneficio de su formación profesional.  
Si solucionó un problema presentado al realizar la práctica también se debe documentar.

## Antes de la práctica: 
La práctica uno me dejó nociones básicas sobre como funciona Docker y la gestión de contenedores, las imagenes utilizadas, etc.Esta gestión de contenedores era básica y bastante limitada teniendo nociones pequeñas de las acciones básicas que se podían emplear, conocimientos de los tópicos tocados en la práctica: a las variables de entorno (tema recurrente en programación y sistemas operativos, variables dinamicas que afectan el comportamiento de los procesos), redes (conocimiento básico sobre como funcionan los puertos), base de datos (puertos de las distintas base de datos, como funcionan algunas como tal), desconozco como controlar estos aspectos con docker, tampoco cómo conectar aplicaciones como WordPress a MySQL mediante contenedores ni cómo manejar puertos y persistencia de datos.

## Luego de la práctica:

### Variables de entorno
Las variables de entorno son utiles para pasar información considerada sensible y aprendí a configurar contenedores. Cree contenedores con imagenes ya utilizadas (nginx), con base de datos (MySQL y Postgres) e incluso con WordPress. Dichos contenedores tenían un modo distinto de configuración para los usuarios, contraseñas y forma de edición

### Redes
   Lo principal hecho fue la creación de redes bridge personalizadas, conectar contenedores a estas redes y cómo los contenedores se comunican internamente. También que un contenedor puede pertenecer a dos de estas mismas, tal como pedía la imagen gracias a 'docker network connect net-curso02 contenedor3'. 
   * Entendí la diferencia entre redes `bridge`, `host` y `none`, y cuándo usar cada una.

### Datos y configuraciones
 Cuando intenté conectar pgAdmin con PostgreSQL, surgió un error de resolución de nombre (`Errno -2 Name does not resolve`). Al consultar con la IA al respecto, me recomendó crear una red personalizada en Docker, esto ayudó a una comunicación eficiente entre ambos contenedores y pude crear la base de datos. 

 Una observación importante fue que al eliminar todo el contenedor de WordPress y volver a crearlo, los datos se conservaron. Algo obvio pues la base de datos se encontraba en otro contenedor pero esta demostración me ayudó a interiorizar el concepto, a su vez, se vio lo importante de separar todo en distintos contenedores para evitar errores en el futuro. 


# Consultar: Cómo se gestionan datos confidenciales con los secretos de Docker (Docker Secrets).

¿De qué trata Docker Secrets? Responsable y el que nos permite almacenar y gestionar los datos cofidenciales. 

 Ese secreto queda guardado en el registro Raft, que se encuentra cifrado. Todo el registro Raft se replica en los demás managers, lo que asegura que los secretos tengan la misma alta disponibilidad que el resto de la información de administración del swarm. Si le das a un servicio —ya sea nuevo o en ejecución— acceso a un secreto, Docker monta el secreto desencriptado dentro del contenedor usando un sistema de archivos en memoria. 

En cualquier momento se puede actualizar un servicio para permitirle acceder a más secretos, o bien quitarle el acceso a alguno.

Un nodo solo puede acceder a los secretos (en su versión cifrada) si es un manager del swarm, o si está ejecutando tareas de servicios que tienen permisos para usar ese secreto. Cuando un contenedor finaliza su ejecución, los secretos desencriptados que se le habían compartido se desmontan del sistema de archivos en memoria y se borran de la memoria del nodo.

Podés agregar o revisar un secreto individual cuando quieras, así como listar todos los secretos existentes. Eso sí, no es posible eliminar un secreto que esté siendo usado por un servicio activo. Para hacerlo sin afectar los servicios, existe la opción de rotar el secreto.