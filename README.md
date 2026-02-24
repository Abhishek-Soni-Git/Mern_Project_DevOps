# MEAN Stack DevOps Deployment

## 🚀 Project Overview

This project demonstrates containerization, CI/CD automation, and cloud deployment of a MEAN (MongoDB, Express, Angular, Node.js) application.

The application has been:

- Containerized using Docker
- Deployed using Docker Compose
- Hosted on AWS EC2 Ubuntu Server
- Automated using Jenkins CI/CD pipeline
- Configured with Nginx Reverse Proxy on port 80

---

## 🏗️ Architecture

GitHub → Jenkins CI/CD → Docker Hub → AWS EC2 → Docker Compose → Nginx → Browser

---

## 🐳 Docker Setup

### Backend
- Node 20 Alpine image
- Runs on port 8080

### Frontend
- Multi-stage build
- Angular build
- Served via Nginx container

---

## 🗄️ Database Setup

MongoDB is deployed using official Docker image via docker-compose.

---

## ☁️ Cloud Infrastructure

- AWS EC2 Ubuntu Server
- Docker & Docker Compose installed
- Security Group allows:
  - Port 22 (SSH)
  - Port 80 (HTTP)

---

## 🔄 CI/CD Pipeline

Implemented using Jenkins.

Pipeline stages:

1. Checkout Code
2. Build Backend Image
3. Build Frontend Image
4. Push Images to Docker Hub
5. SSH into EC2
6. Pull latest images
7. Restart containers

---

## 🌐 Nginx Reverse Proxy

Application accessible via:


http://100.48.91.160
