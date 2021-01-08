FROM maven:3.6.0-jdk-11-slim AS build
COPY . .
RUN mvn -f pom.xml clean package -Dmaven.test.skip=true 
EXPOSE 8080
CMD ["java","-jar","target/tlcdemoApp-1.0.0-SNAPSHOT-runner.jar"]
