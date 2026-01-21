# Lab 5: Multi-Stage Docker Build for Spring Boot App

## Objective
Clone Spring Boot application, create multi-stage Dockerfile for optimized image size, build and run containerized application.

## Prerequisites
- Linux/WSL environment
- Docker installed and running

## Lab Steps

### Step 1: Create Lab Directory and Clone Application
```bash
mkdir lab-5
cd lab-5
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
```

### Step 2: Create Multi-Stage Dockerfile
```dockerfile
FROM maven:3.9.6-eclipse-temurin-17 AS build
WORKDIR /app
COPY Docker-1/ .
RUN mvn package

FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=build /lab5/target/demo-0.0.1-SNAPSHOT.jar .
EXPOSE 8080
CMD ["java", "-jar", "demo-0.0.1-SNAPSHOT.jar"]
```

### Step 3: Build app3 Image
```bash
docker build -t app3 .
```

### Step 4: Run container3 from app3 Image
```bash
docker run -d --name container3 -p 8088:8080 app3:latest
```

### Step 5: Test the Application
```bash
curl http://localhost:8088
```

### Step 6: Stop and Clean Up
```bash
docker stop container3
docker rm container3
```

## Expected Output
<img width="911" height="460" alt="Lab-5 1" src="https://github.com/user-attachments/assets/b5405a93-ab51-4980-bfac-c59cb0ef0fbe" />
<img width="715" height="149" alt="lab-5 2" src="https://github.com/user-attachments/assets/b7750a45-eb3c-4c29-a722-53f2748eacec" />
<img width="1433" height="402" alt="lab5 3" src="https://github.com/user-attachments/assets/7e4a98ee-9d8f-4cca-9054-48cbbad37f07" />




## Author
**Nour Eldeen Mohamed** 
