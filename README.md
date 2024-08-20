
Certainly! Here’s the updated README with additional information about phpMyAdmin:

---

# LEMP Stack with Docker

This repository contains a Docker-based LEMP (Linux, Nginx, MySQL, PHP) stack setup. It provides a structured environment for developing and deploying PHP applications with Nginx and MySQL, using Docker to manage the environment and dependencies.

## Table of Contents

- [LEMP Stack with Docker](#lemp-stack-with-docker)
  - [Table of Contents](#table-of-contents)
  - [Project Structure](#project-structure)
  - [Getting Started](#getting-started)
  - [Configuration](#configuration)
  - [Usage](#usage)
  - [Docker Services](#docker-services)
  - [phpMyAdmin](#phpmyadmin)
  - [Docker Commands](#docker-commands)
  - [License](#license)
  - [Contributing](#contributing)
  - [Contact](#contact)

## Project Structure

```
├── README.md                 # Project documentation
├── docker-compose.yml        # Docker Compose configuration
├── dockerfiles
│   └── php.dockerfile         # Dockerfile for PHP
├── nginx
│   └── default.conf           # Nginx configuration
├── php
│   └── php.ini                # PHP configuration
├── src
│   └── index.php              # Sample PHP application
└── storage
    └── README.md             # Storage directory placeholder
```

## Getting Started

To get started with this LEMP stack, follow these steps:

1. **Clone the Repository**

   ```bash
   git clone https://github.com/HamaDevek/LEMP-Stack-Docker.git
   cd LEMP-Stack-Docker
   ```

2. **Build and Run the Docker Containers**

   ```bash
   docker-compose up --build
   ```

   This command will build the Docker images and start the containers defined in `docker-compose.yml`.

3. **Access the Application**

   Once the containers are up, you can access the application by navigating to `http://localhost:3333` in your web browser. phpMyAdmin can be accessed at `http://localhost:8080`.

## Configuration

- **Nginx**: Configuration can be found in `nginx/default.conf`. Modify this file to adjust server settings or add additional server blocks.
- **PHP**: PHP settings are defined in `php/php.ini`. Customize PHP configurations as needed.
- **MySQL**: Database settings can be adjusted in `docker-compose.yml` under the `mysql` service section.

## Usage

- **Adding PHP Files**: Place your PHP files in the `src` directory. These will be served by Nginx.
- **Persistent Storage**: Files in the `storage` directory are excluded from version control but can be used for persistent application data.

## Docker Services

The `docker-compose.yml` file defines the following services:

- **nginx**
  - **Image**: `nginx:latest`
  - **Container Name**: `nginx`
  - **Ports**: `3333:80` (host:container)
  - **Volumes**:
    - `./src:/var/www/html:delegated`
    - `./nginx/default.conf:/etc/nginx/conf.d/default.conf`
  - **Depends On**: `php`, `mysql`
  - **Networks**: `app-network`

- **mysql**
  - **Image**: `mysql:latest`
  - **Restart Policy**: `unless-stopped`
  - **Container Name**: `mysql`
  - **Ports**: `3304:3306` (host:container)
  - **Volumes**:
    - `./storage:/var/lib/mysql`
  - **Environment Variables**:
    - `MYSQL_ROOT_PASSWORD`: your_root_password
    - `MYSQL_DATABASE`: your_database_name
    - `MYSQL_USER`: your_database_user
    - `MYSQL_PASSWORD`: your_database_password
  - **Networks**: `app-network`

- **php**
  - **Build Context**: `./dockerfiles`
  - **Dockerfile**: `php.dockerfile`
  - **Volumes**:
    - `./php/php.ini:/usr/local/etc/php/php.ini`
    - `./src:/var/www/html:delegated`
  - **Networks**: `app-network`

- **phpmyadmin**
  - **Container Name**: `phpmyadmin`
  - **Depends On**: `mysql`
  - **Image**: `phpmyadmin/phpmyadmin`
  - **Restart Policy**: `always`
  - **Ports**: `8080:80` (host:container)
  - **Environment Variables**:
    - `PMA_HOST`: mysql
  - **Networks**: `app-network`

## phpMyAdmin

**phpMyAdmin** is a web-based tool for managing MySQL databases. It provides a user-friendly interface to interact with your databases, making tasks such as creating, modifying, and deleting databases and tables more accessible. It also allows for executing SQL queries directly and managing user privileges.

- **Access phpMyAdmin**: Navigate to `http://localhost:8080` in your web browser.
- **Login**: Use the credentials defined in the `mysql` service of `docker-compose.yml`:
  - **Username**: `your_database_user`
  - **Password**: `your_database_password`
- **Features**:
  - Browse and manage your database tables
  - Execute SQL queries and import/export databases
  - Manage user accounts and permissions

## Docker Commands

- **Build Images**: `docker-compose build`
- **Start Containers**: `docker-compose up`
- **Stop Containers**: `docker-compose down`
- **View Logs**: `docker-compose logs`
- **Access Container Shell**: `docker-compose exec <service> bash`

Replace `<service>` with the name of the service you want to access (e.g., `php` or `mysql`).

## License

This project is licensed under the [MIT License](LICENSE).

## Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Commit your changes (`git commit -am 'Add new feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Create a new Pull Request.

## Contact

For questions or comments, please contact:

- **Name**: Mohammed Kamaran
- **Email**: dv.hamakamaran@gmail.com
- **GitHub**: [HamaDevek](https://github.com/HamaDevek)

---