# TODO

# We use Maven version 3.6.3 for the build, with JDK 11.
FROM maven:3.6.3-jdk-11 AS builder
# Run the build scripts:
#  - src/products-api/restore.sh
#  - src/products-api/build.sh
#  you'll need to make the files executable first with chmod +x <filename>.
WORKDIR /usr/src/api
COPY src/products-api/. .
RUN chmod +x restore.sh && ./restore.sh
RUN chmod +x build.sh  && ./build.sh
    
# Build output is a single JAR file:
#  /usr/src/api/target/products-api-0.1.0.jar
# The app should run on OpenJDK 11.0.12, it can use a minimal OS. 
FROM openjdk:11.0.12-jre-slim-buster
WORKDIR /app
COPY --from=builder  /usr/src/api/target/products-api-0.1.0.jar .

EXPOSE 80
ENTRYPOINT ["java", "-jar", "/app/products-api-0.1.0.jar"]
# We need to set two environment variables - 
# JRE_VERSION and APP_VERSION. 
ENV JRE_VERSION="11.0.1"\
    APP_VERSION="0.4.0"
# The startup command needs to run the JAR file from the build:

#  java -jar products-api-0.1.0.jar
