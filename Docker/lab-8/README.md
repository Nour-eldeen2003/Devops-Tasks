# Lab 8: Custom Docker Network for Microservices

## Objective
Create custom Docker network and verify container communication between frontend and backend microservices.

## Prerequisites
- Linux/WSL environment
- Docker installed and running

## Lab Steps

### Step 1: Create Lab Directory
```bash
mkdir lab-8
cd lab-8
```

### Step 2: Clone Repository
```bash
git clone https://github.com/Ibrahim-Adel15/Docker5.git
cd Docker5
```

### Step 3: Create Dockerfile for Frontend
```bash
FROM python:3.9-slim
WORKDIR /app
RUN pip install flask requests
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]
```

### Step 4: Create Dockerfile for Backend
```bash
FROM python:3.9-slim
WORKDIR /app
COPY . .
RUN pip install flask
EXPOSE 5000
CMD ["python", "app.py"]
```

### Step 5: Build Frontend Image
```bash
docker build -t front-image .
```

### Step 6: Build Backend Image
```bash
docker build -t back-image .
```

### Step 7: Configure Orchestration (docker-compose.yml)
```bash
services:
  frontend-service:
    build: ./frontend
    image: frontend-image
    ports:
      - "5001:5000"
    environment:
      - BACKEND_URL=http://backend-service:5000
    networks:
      - custom-net
    depends_on:
      - backend-service

  backend-service:
    build: ./backend
    image: backend-image
    ports:
      - "5002:5000"
    networks:
      - custom-net

networks:
  custom-net:
    name: ivolve-network
    driver: bridge
```

### Step 8: Deploy the Stack
```bash
sudo docker compose up -d --build --force-recreate
```

### Step 9: Verify Containers and Network
```bash
sudo docker compose ps
sudo docker network ls
```

### Step 10: Test Communication - Frontend1 to Backend (Should Work)
```bash
sudo docker compose exec frontend-service sh
ping -c 3 backend-service
```

### Step 11: Test Communication - Frontend2 to Backend (Should Fail)
```bash
sudo docker compose exec backend-service bash
ping -c 3 frontend-service
```

### Step 12: Inspect Network
```bash
docker network inspect ivolve-network
```

### Step 13: Cleanup
```bash
sudo docker compose down
```

### Step 14: Delete Custom Network
```bash
docker network rm ivolve-network
```

### Step 15: Verify Network Deletion
```bash
docker network ls
```

## Expected Results
<img width="1796" height="188" alt="lab-8 5" src="https://github.com/user-attachments/assets/5f9e2db7-cf29-4854-9bd4-3ba204eed645" />
<img width="1573" height="50" alt="lab-8 4" src="https://github.com/user-attachments/assets/0c59032f-2135-4748-9751-198239194f92" />
<img width="1918" height="948" alt="lab-8 3" src="https://github.com/user-attachments/assets/7b80af80-999e-45dc-adb9-211cf91b0d13" />
<img width="1906" height="77" alt="lab-8 2" src="https://github.com/user-attachments/assets/48fdc3b5-438e-48b9-982c-efd4d5c16b51" />
<img width="1906" height="108" alt="lab-8 1" src="https://github.com/user-attachments/assets/efbd35b9-fe0e-4710-874d-06d1f91f9076" />

## Author
**Nour Eldeen Mohamed**
