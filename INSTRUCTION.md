# Container Management Instructions (todoapp)

This document details all necessary commands for managing your multi-container project using **Docker Compose**. All commands should be executed from the project's root directory where the `docker-compose.yml` file is located.

## Prerequisites

Ensure both **Docker** and **Docker Compose** are installed and running on your system.

## Core Commands

**Initial Launch and Build (`up --build -d`):**
This is the command for the very first launch or whenever source code, dependencies, or Dockerfiles have been modified. It forces a rebuild of the application image (`todoapp`), then creates and starts all services (including `mysql`) in the background (`-d`).
`docker-compose up --build -d`

**Start Stopped Containers (`up -d`):**
Use this for quick restarts when the containers were stopped previously, and no rebuild is required. It reads the existing image and starts the services in the background.
`docker-compose up -d`

**Stop Containers (`stop`):**
Halts the running containers gracefully but keeps them on your system along with all associated data volumes (like `mysql_data`). The containers can be quickly restarted later.
`docker-compose stop`

**Stop and Remove (Preserve Data) (`down`):**
Stops and completely removes all containers, as well as the defined networks. Importantly, by default, it **preserves** the named data volume (`mysql_data`).
`docker-compose down`

**Stop and Remove (Delete Data Volume) (`down --volumes`):**
Stops and removes containers, networks, **AND** forces the deletion of all named data volumes (including `mysql_data`). **Use with extreme caution, as all database data will be lost.**
`docker-compose down --volumes`

## Utility Commands

**View Container Status (`ps`):**
Displays a list of all services defined in the configuration and their current status (running, stopped, etc.).
`docker-compose ps`

**View Live Logs (All Services) (`logs -f`):**
Streams the output (logs) from all running services to the terminal in real-time. This is essential for monitoring startup and debugging.
`docker-compose logs -f`

**View Live Logs (Specific Service) (`logs -f <service_name>`):**
Streams logs only from the specified service (e.g., `todoapp` or `mysql`).
`docker-compose logs -f todoapp`

**Execute Interactive Command (`exec <service_name> <command>`):**
Runs an arbitrary command inside a running service container. Ideal for maintenance or debugging tasks.

* **Example: Get a Bash Shell:**
    `docker-compose exec todoapp bash`

* **Example: Run Django Superuser Creation:**
    `docker-compose exec todoapp python manage.py createsuperuser`