# MEAN Stack CRUD Application with Docker

This project is a full-stack CRUD (Create, Read, Update, Delete) application built using the MEAN stack (MongoDB, Express.js, Angular, Node.js) and containerized with Docker.

## Prerequisites

- Node.js (v18 or later)
- Docker and Docker Compose
- Angular CLI
- MongoDB
- Git
- AWS Account (for EC2 deployment)

## Project Structure

```
.
├── frontend/               # Angular frontend application
├── backend/               # Node.js/Express backend API
├── docker-compose.yml    # Docker compose configuration
└── README.md
```

## Local Development Setup

1. Clone the repository:

   ```bash
   git clone <your-repository-url>
   cd crud-dd-task-mean-app
   ```

2. Backend Setup:

   ```bash
   cd backend
   npm install
   npm start
   ```

3. Frontend Setup:
   ```bash
   cd frontend
   npm install
   ng serve
   ```

The application will be available at:

- Frontend: http://localhost:4202
- Backend API: http://localhost:8080
- MongoDB: mongodb://localhost:27017

## Docker Deployment

1. Build and run using Docker Compose:

   ```bash
   docker compose up -d --build
   ```

2. Stop the containers:
   ```bash
   docker compose down
   ```

Services will be available at:

- Frontend: http://localhost:4202
- Backend API: http://localhost:8080
- MongoDB: mongodb://localhost:27017

## AWS EC2 Deployment

1. Launch an EC2 instance:

   - Use Ubuntu Server 22.04 LTS
   - Configure Security Group with the following inbound rules:
     - SSH (22): Your IP
     - HTTP (80): 0.0.0.0/0
     - Custom TCP (4202): 0.0.0.0/0
     - Custom TCP (8080): 0.0.0.0/0
     - Custom TCP (27017): 0.0.0.0/0

2. Connect to your EC2 instance:

   ```bash
   ssh -i your-key.pem ubuntu@your-ec2-public-ip
   ```

3. Install Docker and Docker Compose:

   ```bash
   # Update package list
   sudo apt update

   # Install Docker
   sudo apt install docker.io -y

   # Install Docker Compose
   sudo apt install docker-compose -y

   # Add user to docker group
   sudo usermod -aG docker $USER

   # Log out and log back in for changes to take effect
   exit
   ```

4. Clone and deploy the application:

   ```bash
   # Clone repository
   git clone <your-repository-url>
   cd crud-dd-task-mean-app

   # Start the containers
   docker compose up -d
   ```

The application will be available at:

- Frontend: http://your-ec2-public-ip:4202
- Backend API: http://your-ec2-public-ip:8080

## API Endpoints

The backend provides the following RESTful endpoints:

- `GET /api/tutorials`: Get all tutorials
- `GET /api/tutorials/:id`: Get tutorial by ID
- `POST /api/tutorials`: Create new tutorial
- `PUT /api/tutorials/:id`: Update tutorial by ID
- `DELETE /api/tutorials/:id`: Delete tutorial by ID
- `DELETE /api/tutorials`: Delete all tutorials

## Environment Variables

Backend environment variables (`.env`):

```
DB_URL=mongodb://mongodb:27017/tutorial_db
```

Docker environment variables:

```
MONGODB_PORT=27017
BACKEND_PORT=8080
FRONTEND_PORT=4202
```

## Troubleshooting

1. If containers fail to start:

   ```bash
   # Check container logs
   docker logs app-frontend-1
   docker logs app-backend-1
   docker logs app-mongodb-1
   ```

2. If you can't connect to the application:
   - Verify all ports are open in your EC2 security group
   - Check if containers are running: `docker ps`
   - Ensure no port conflicts with local services

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.
