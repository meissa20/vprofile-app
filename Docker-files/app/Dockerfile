FROM maven:3.9.9-eclipse-temurin-21 AS builder
ENV MAVEN_OPTS="-Xms256m -Xmx2048m"
WORKDIR /build
COPY pom.xml .
COPY src ./src
RUN mvn --batch-mode --no-transfer-progress clean package -DskipTests

FROM tomcat:11.0-jdk21-temurin-noble
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=builder /build/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
