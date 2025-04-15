FROM openjdk:21
VOLUME /tmp
COPY app/target/*.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
