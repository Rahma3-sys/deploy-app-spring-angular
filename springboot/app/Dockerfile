
# Étape 1 : builder avec Maven
FROM maven:3.9.1-eclipse-temurin-17 AS build
WORKDIR /app

# Copier pom.xml et src
COPY pom.xml .
COPY src ./src

# Compiler le projet (ignore les tests pour aller plus vite)
RUN mvn clean package -DskipTests

# Étape 2 : image finale Java
FROM openjdk:17-jdk-slim
WORKDIR /app

# Copier le JAR construit depuis l'étape précédente
COPY --from=build /app/target/*.jar app.jar

# Exposer le port
EXPOSE 8081

# Lancer l'application
ENTRYPOINT ["java","-jar","/app.jar"]
