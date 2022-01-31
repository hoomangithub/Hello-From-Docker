# Spring Boot with JIB (Docker)

### setting.xml for Maven

    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
        xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 https://maven.apache.org/xsd/settings-1.0.0.xsd">
        
        <localRepository>${user.home}/.m2/repository</localRepository>
	    <interactiveMode>true</interactiveMode>
	    <offline>false</offline>
        
        <servers>
            <server>
                <id>registry.hub.docker.com</id>
                <username>UUUUUUU</username>
                <password>PPPPPPP</password>
            </server>
            <server>
                <id>quay.io</id>
                <username>UUUUUUU</username>
                <password>PPPPPPP</password>
            </server>		
        </servers>

## Build Docker Image from Standard Jib Image (Ubuntu)
> mvn compile jib:dockerBuild -PJib

## Build Docker Image from BaseImage

### Build and Push Docker BaseImage
> - Rename Dockerfiles/Dockerfile_openjdk11_Baseimage.txt to **Dockerfile**
> - docker login quay.io
> - docker build -t quay.io/hoomi71/openjdk11.0.13-jre-slim_base:310122 .
> - docker push quay.io/hoomi71/openjdk11.0.13-jre-slim_base:310122

### Build Application Docker with JIB Maven Plugin from BaseImage

> mvn compile jib:build -PJibCustomized

## Run Container
> docker run -d -p 8082:8080 quay.io/hoomi71/hello_from_openjdk11:**TAG**
 
## Call Application
- http://localhost:8082/hello 
- http://localhost:8082/hello?name=Hooman
