# Lab 4: Build and Run Spring Boot App with Optimized Docker Image

## Objective
Clone Spring Boot application, build with Maven, create optimized Dockerfile, and run containerized application.

## Prerequisites
- Linux/WSL environment
- Docker installed and running
- Maven installed

## Lab Steps

### Step 1: Create Lab Directory and Clone Application
```bash
mkdir docker/lab-4
cd docker/lab-4
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1
```

### Step 2: Build Application with Maven
```bash
mvn package
```

### Step 3: Create Dockerfile
```dockerfile
FROM eclipse-temurin:17-jre-alpine
WORKDIR /lab4
COPY target/demo-0.0.1-SNAPSHOT.jar .
CMD ["java", "-jar", "demo-0.0.1-SNAPSHOT.jar"]
EXPOSE 8080
```

### Step 4: Build app2 Image
```bash
docker build -t app2 .
```

### Step 5: Run container2 from app2 Image
```bash
docker run -d --name container2 -p 8088:8080 app2:latest
```

### Step 6: Test the Application
```bash
curl http://localhost:8088
```

### Step 7: Stop and Remove Container
```bash
docker stop container2
docker rm container2
```

## Expected Output
<img width="1381" height="758" alt="Screenshot From 2026-01-19 18-50-32" src="https://github.com/user-attachments/assets/785fe5d9-d627-4e2e-a081-092e8660ecf9" />
<img width="536" height="151" alt="image" src="https://github.com/user-attachments/assets/eaa71854-4a20-41ec-b584-c98c482ef008" />





## Author
**Nour Eldeen Mohamed** 
