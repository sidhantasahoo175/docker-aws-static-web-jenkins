# Docker AWS Static Web Application

A static web application containerized with Docker, pushed to Docker Hub, and deployed on an AWS EC2 instance.

## Local run

```powershell
docker build -t your-dockerhub-username/docker-aws-static-web:latest .
docker run -d --name static-web -p 8000:80 your-dockerhub-username/docker-aws-static-web:latest
```

Open: http://localhost:8000

## Docker Hub

```powershell
docker login
docker push your-dockerhub-username/docker-aws-static-web:latest
```

## EC2

After installing Docker on the EC2 instance:

```bash
docker pull your-dockerhub-username/docker-aws-static-web:latest
docker run -d --name static-web -p 8000:80 your-dockerhub-username/docker-aws-static-web:latest
```

Open:

`http://YOUR_EC2_PUBLIC_IP:8000`
