# devops-container-p1
devops-container-p1 Ankit Ulak

# Dockerized Laravel & Vue Application

This repository contains a full-stack application setup for the CloudTech Services internship task. It orchestrates a **Laravel (Backend)**, **Vue.js (Frontend)**, **Nginx**, and **MySQL** database using Docker Compose.

## 📂 Project Structure
- **backend/**: Laravel 10 application (API/Backend) running on PHP 8.2-FPM.
- **frontend/**: Vue.js 3 application running on Nginx (Multi-stage build).
- **nginx/**: Configuration for the backend web server.
- **docker-compose.yml**: Orchestration for all services.

## 🚀 Setup Guide

### Prerequisites
- Docker & Docker Compose installed.

## Installation Steps

1. **Clone the Repository**
   ```bash
   git clone [https://github.com/DemiAnkit/devops-container-p1.git]
   cd [devops-container-p1]
   ```

2. **Configure Environment**
    Navigate to the backend and set up the .env file:
    ```bash
    cd backend
    cp .env.example .env
    ```

 ## Important: Open .env and ensure the database connection matches the Docker service:

    ```bash
    DB_CONNECTION=mysql
    DB_HOST=db
    DB_PORT=3306
    DB_DATABASE=laravel_db
    DB_USERNAME=laravel_user
    DB_PASSWORD=userpassword
    ```

3. **Start the Application**

 ## Return to the root directory and build the containers:

    ```bash
    docker-compose up -d --build
    ```

**or**

    ```bash
    docker-compose build --no-cache app
    docker-compose up -d
    docker-compose up -d --build

    ```

**Initialize Backend**
## Once containers are running, run these commands to set up Laravel keys and database tables:

    ```bash
    docker-compose exec app php artisan key:generate
    docker-compose exec app php artisan migrate
    ```

**Fix Windows Permissions (Crucial)**
## Since you are on Windows, the website might show a "Permission Denied" error if you don't run this:
    ```bash
    docker-compose exec app chmod -R 777 storage bootstrap/cache
    ```

   