# Variables de Entorno

### ¿Qué son las variables de entorno?
Valores dinámicos que pueden afectar el comportamiento de procesos en un sistema operativo o en contenedores. Se utilizan para configurar aplicaciones sin modificar el código fuente.

### Para crear un contenedor con variables de entorno

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.

```
docker run -d --name nginx_env -e username=bell -e role=admin nginx:alpine
```

# CAPTURA CON LA COMPROBACIÓN DE LA CREACIÓN DE LAS VARIABLES DE ENTORNO DEL CONTENEDOR ANTERIOR

![alt text](image-1.png)

### Crear un contenedor con la imagen de mysql, mapear todos los puertos

```
docker run -d --name mysql_container -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 mysql:latest
```

### ¿El contenedor se está ejecutando?

![alt text](image-2.png)
Como sale Up, significa que está ejecutando.


### Para crear un contenedor con variables de entorno especificadas
- Portabilidad: Las aplicaciones se vuelven más portátiles y pueden ser desplegadas en diferentes entornos (desarrollo, pruebas, producción) simplemente cambiando el archivo de variables de entorno.
- Centralización: Todas las configuraciones importantes se centralizan en un solo lugar, lo que facilita la gestión y auditoría de las configuraciones.
- Consistencia: Asegura que todos los miembros del equipo de desarrollo o los entornos de despliegue utilicen las mismas configuraciones.
- Evitar Exposición en el Código: Mantener variables sensibles como contraseñas, claves API, y tokens fuera del código fuente reduce el riesgo de exposición accidental a través del control de versiones.
- Control de Acceso: Los archivos de variables de entorno pueden ser gestionados con permisos específicos, limitando quién puede ver o modificar la configuración sensible.

### ¿Qué bases de datos existen en el contenedor creado?

```
SHOW DATABASE
```

![alt text](image-3.png)
