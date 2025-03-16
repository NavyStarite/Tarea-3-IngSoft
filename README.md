# Tarea-3-IngSoft
Tarea 3.- Dockerización y Conexión con Base de Datos

Alumno: Sanchez Gonzalez Daniel Ivan

# IngenieriaSoftwareTarea3

## Tecnologías Utilizadas

El proyecto utiliza las siguientes tecnologías:

- **Java 21** (Amazon Corretto)
- **Spring Boot**
- **Maven 3.9.9**
- **Docker**
- **VS Code**

## Requisitos Previos

Para ejecutar este proyecto en tu entorno local, asegúrate de contar con los siguientes componentes instalados:

- **Java 21** (Amazon Corretto)
- **Maven 3.9.9**
- **Docker**

## Clonar el Repositorio

Para obtener una copia local del proyecto, ejecuta:

```sh
git clone https://github.com/NavyStarite/Tarea-3-IngSoft.git
cd tu-repositorio
```

## Compilar y Ejecutar la Aplicación

Si deseas ejecutar la aplicación sin utilizar Docker, usa el siguiente comando:

```sh
mvn spring-boot:run
```

**Nota:** Se ha utilizado **XAMPP** junto con **phpMyAdmin** como base de datos. Puedes encontrar los comandos SQL necesarios para crear la base de datos en el archivo `bd.sql`.

## Ejecutar con Docker

Para desplegar la aplicación con Docker, sigue estos pasos:

### Construcción y Ejecución

Ejecuta el siguiente comando para construir y ejecutar los contenedores:

```sh
docker-compose up --build
```

La aplicación estará disponible en: [http://localhost:18080/home](http://localhost:18080/home).

## Capturas de Pantalla



## Investigación

El proyecto emplea Docker para la contenedorización, optimizando su despliegue en cualquier entorno. Se han utilizado dos archivos clave:

### Dockerfile

El **Dockerfile** define el proceso de construcción de la imagen en dos etapas:

1. **Etapa de compilación**: Se usa una imagen base de Maven para compilar el código. Se copian `pom.xml` y las dependencias necesarias, luego se añade el código fuente y se ejecuta la compilación con Maven para generar el archivo `.jar`.
2. **Etapa de ejecución**: Se emplea una imagen optimizada de Java (`eclipse-temurin:21-jre`) sin herramientas de desarrollo innecesarias. Se copia el `.jar` generado en la etapa anterior y se configura el contenedor para exponer el puerto 8080 y ejecutar la aplicación con:
   ```sh
   java -jar app.jar
   ```

Este enfoque minimiza el tamaño de la imagen final y mejora la eficiencia en su ejecución.

### docker-compose.yml

El archivo **docker-compose.yml** gestiona la ejecución de los contenedores de la aplicación y la base de datos. Define dos servicios principales:

- **Aplicación (app)**: Se construye a partir del Dockerfile y expone el puerto 8080. Se asegura de que la base de datos esté disponible antes de iniciar.
- **Base de datos (db)**: Utiliza la imagen oficial de MySQL 8.0. Se configuran credenciales a través de variables de entorno y se asigna un volumen (`mysql-data`) para la persistencia de datos. Al iniciar, se carga el archivo `bd.sql` con la estructura de la base de datos.


