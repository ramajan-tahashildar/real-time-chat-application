# Real-Time Chat Application

A full-stack, real-time chat application built with **React**, **Node.js**, **Express**, **MongoDB**, **Socket.io**, and **Kubernetes**. This project demonstrates modern web development practices, including authentication, real-time messaging, containerization, and orchestration.

---

## Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Environment Variables](#environment-variables)
  - [Running Locally](#running-locally)
  - [Docker Usage](#docker-usage)
  - [Kubernetes Deployment](#kubernetes-deployment)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

---

## Features

- **Real-time Messaging:** Instant chat using Socket.io.
- **User Authentication:** Secure login/signup with JWT and hashed passwords.
- **Profile Management:** Users can upload and update their profile pictures.
- **Online Status:** See which users are online in real-time.
- **Modern UI:** Responsive interface with React, TailwindCSS, and DaisyUI.
- **Containerization:** Docker support for both frontend and backend.
- **Orchestration:** Kubernetes manifests for scalable deployment.
- **State Management:** Zustand for frontend state.
- **API Security:** Uses HTTP-only cookies and CORS.

---

## Architecture

- **Frontend:** React SPA served by Nginx, communicates with backend via REST API and Socket.io.
- **Backend:** Express server with REST endpoints and Socket.io for real-time communication.
- **Database:** MongoDB for persistent storage.
- **Containerization:** Dockerfiles for both frontend and backend.
- **Orchestration:** Kubernetes manifests for deployments, services, ingress, and persistent storage.

---

## Tech Stack

- **Frontend:** React, Vite, TailwindCSS, DaisyUI, Zustand, React Router, Lucide Icons
- **Backend:** Node.js, Express, MongoDB, Mongoose, Socket.io, JWT, Cloudinary (for image uploads)
- **DevOps:** Docker, Kubernetes, Nginx

---

## Project Structure

```
chat-application/
├── backend/
│   ├── src/
│   │   ├── controllers/
│   │   ├── lib/
│   │   ├── middleware/
│   │   ├── models/
│   │   ├── routes/
│   │   └── index.js
│   ├── Dockerfile
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── store/
│   │   ├── lib/
│   │   └── App.jsx
│   ├── public/
│   ├── Dockerfile
│   ├── nginx.conf
│   └── package.json
├── k8s/
│   ├── backend-deployment.yml
│   ├── backend-service.yml
│   ├── frontend-deployment.yml
│   ├── frontend-service.yml
│   ├── ingress.yml
│   ├── mongoDB-deployment.yml
│   ├── mongoDB-pv.yml
│   ├── mongoDB-pvc.yml
│   ├── mongoDB-service.yml
│   └── namespace.yml
├── README.md
└── package.json
```

---

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v14+)
- [Docker](https://www.docker.com/get-started)
- [Kubernetes](https://kubernetes.io/) (for orchestration)
- [MongoDB](https://www.mongodb.com/) (local or Docker)

### Environment Variables

Create a `.env` file in the `backend/` directory:

```env
MONGODB_URI=mongodb://mongo:27017/chatapp
JWT_SECRET=your_jwt_secret_key
PORT=5001
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

> Replace the Cloudinary variables with your own if you want to enable image uploads.

### Running Locally

#### 1. Clone the repository

```sh
git clone https://github.com/yourusername/chat-application.git
cd chat-application
```

#### 2. Install dependencies

```sh
cd backend && npm install
cd ../frontend && npm install
```

#### 3. Start MongoDB

- Locally: `mongod`
- Or with Docker:  
  `docker run -d -p 27017:27017 --name mongo mongo:latest`

#### 4. Start Backend

```sh
cd backend
npm run dev
```

#### 5. Start Frontend

```sh
cd frontend
npm run dev
```

- Frontend: [http://localhost:5173](http://localhost:5173)
- Backend API: [http://localhost:5001/api](http://localhost:5001/api)

---

### Docker Usage

#### Build and Run with Docker Compose

You can use Docker Compose (add a `docker-compose.yml` if needed) or run containers manually:

```sh
# Build images
docker build -t chat-frontend ./frontend
docker build -t chat-backend ./backend

# Create network
docker network create chat-net

# Run MongoDB
docker run -d --network=chat-net --name mongo mongo:latest

# Run Backend
docker run -d --network=chat-net --env-file ./backend/.env -p 5001:5001 --name backend chat-backend

# Run Frontend
docker run -d --network=chat-net -p 5173:80 --name frontend chat-frontend
```

---

### Kubernetes Deployment

1. Make sure your cluster is running and `kubectl` is configured.
2. Apply the namespace:

   ```sh
   kubectl apply -f k8s/namespace.yml
   ```

3. Deploy MongoDB (PV, PVC, Deployment, Service):

   ```sh
   kubectl apply -f k8s/mongoDB-pv.yml
   kubectl apply -f k8s/mongoDB-pvc.yml
   kubectl apply -f k8s/mongoDB-deployment.yml
   kubectl apply -f k8s/mongoDB-service.yml
   ```

4. Deploy Backend and Frontend:

   ```sh
   kubectl apply -f k8s/backend-deployment.yml
   kubectl apply -f k8s/backend-service.yml
   kubectl apply -f k8s/frontend-deployment.yml
   kubectl apply -f k8s/frontend-service.yml
   ```

5. Deploy Ingress (update host as needed):

   ```sh
   kubectl apply -f k8s/ingress.yml
   ```

---

## Usage

- **Sign Up:** Create a new account.
- **Login:** Access your chat dashboard.
- **Chat:** Select a user from the sidebar and start messaging in real-time.
- **Profile:** Update your profile picture and view account info.
- **Settings:** Change the chat theme.

---

## Contributing

Contributions are welcome! Please open issues and submit pull requests for improvements or bug fixes.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---