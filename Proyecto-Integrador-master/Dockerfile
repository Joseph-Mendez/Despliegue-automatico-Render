# Usamos una imagen base de OpenJDK para construir el proyecto
FROM maven:3.8.4-openjdk-17 AS build

# Establecemos el directorio de trabajo
WORKDIR /app

# Copiamos el archivo pom.xml y descargamos las dependencias
COPY pom.xml .
RUN mvn dependency:go-offline

# Copiamos el código fuente
COPY src /app/src

# Construimos el proyecto
RUN mvn clean package

# Usamos una imagen base de OpenJDK para ejecutar el proyecto
FROM openjdk:17-jdk-slim

# Establecemos el directorio de trabajo
WORKDIR /app

# Copiamos el JAR construido desde la etapa anterior
COPY --from=build /app/target/your-app.jar app.jar

# Exponemos el puerto en el que la aplicación se ejecutará
EXPOSE 8080

# Comando para ejecutar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]