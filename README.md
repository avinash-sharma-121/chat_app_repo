# 🗨️ Full-Stack Chat Application

This is a modern full-stack chat application featuring real-time messaging, user authentication, and media sharing. The project is built with a React + Vite frontend, an Express/Node.js backend, and MongoDB for data storage. It supports deployment via Kubernetes (Kind), Docker Compose, and Helm.

---

## 🚀 Features
- Real-time chat with Socket.IO
- User authentication (signup, login, logout)
- Profile management
- Media (image) upload via Cloudinary
- Responsive UI with Tailwind CSS
- Modern React (hooks, Zustand state management)

---

## 🛠️ Tech Stack
- **Frontend:** React, Vite, Tailwind CSS, Zustand, Axios, Socket.IO Client
- **Backend:** Node.js, Express, Socket.IO, Mongoose, JWT, Cloudinary
- **Database:** MongoDB
- **DevOps:** Docker, Docker Compose, Kubernetes (Kind), Helm

---

## 📁 Project Structure
```
chat_app_repo/
├── backend/      # Express backend API
├── frontend/     # React frontend app
├── k8s/          # Kubernetes manifests
├── helm_chat_app/# Helm chart for K8s
├── docker-compose.yml
└── jenkinfile

```

---

## ⚡ Quick Start (Local)

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd chat_app_repo
```

### 2. Start with Docker Compose
```bash
docker-compose up -d --build
```
Access the app at [http://localhost:8080](http://localhost:8080)

---

## ☸️ Kubernetes Deployment (Kind)
See [k8s/README.md](k8s/README.md) for a detailed step-by-step guide to deploy using Kind and kubectl.

---

## 🧩 Backend Overview
- REST API for authentication and messaging
- Real-time communication with Socket.IO
- MongoDB for user and message storage
- JWT-based authentication

**Run locally:**
```bash
cd backend
npm install
npm run dev
```

---

## 🖥️ Frontend Overview
- Built with React, Vite, Zustand, Tailwind CSS
- Auth, chat, profile, and settings pages

**Run locally:**
```bash
cd frontend
npm install
npm run dev
```

---

## 📝 Contributing
Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change.

---

## 📄 License
This project is licensed under the ISC License.
