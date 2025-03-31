# Docker LEMP Stack

This is a LEMP (Linux, Nginx, MariaDB, PHP) stack running in Docker containers.

## Components
- Nginx (Latest)
- PHP 8.3-FPM
- MariaDB (Latest)
- phpMyAdmin
- WP-CLI (WordPress Command Line Interface)

## Configuration
- Environment variables are stored in `.env` file
- Default configuration:
  - Nginx runs on port 80
  - phpMyAdmin runs on port 8080
  - MariaDB credentials:
    - Root password: your_root_password
    - Database: app_db
    - User: app_user
    - Password: app_password

## Environment Variables
The project uses a `.env` file for configuration. You can copy the `.env.example` file to create your own `.env` file:

```bash
cp .env.example .env
```

Available environment variables:
- `NGINX_PORT`: The port Nginx will listen on (default: 80)
- `PHP_VERSION`: PHP version to use (default: 8.3-fpm)
- `MARIADB_VERSION`: MariaDB version to use (default: latest)
- `MYSQL_ROOT_PASSWORD`: MariaDB root password
- `MYSQL_DATABASE`: Default database name
- `MYSQL_USER`: Database user
- `MYSQL_PASSWORD`: Database password
- `PMA_PORT`: phpMyAdmin port (default: 8080)

## Usage
1. Configure your environment:
   ```bash
   cp .env.example .env
   # Edit .env file if needed
   ```

2. Start the containers:
   ```bash
   docker-compose up -d
   ```

3. Access the services:
   - Website: http://localhost
   - phpMyAdmin: http://localhost:8080

4. Using WP-CLI:
   ```bash
   # Example: Check WP-CLI version
   docker-compose exec php wp --info
   
   # Example: Install WordPress
   docker-compose exec php wp core download
   docker-compose exec php wp config create --dbname=app_db --dbuser=app_user --dbpass=app_password --dbhost=mariadb
   docker-compose exec php wp core install --url=localhost --title="WordPress Site" --admin_user=admin --admin_password=admin_password --admin_email=admin@example.com
   ```

5. Stop the containers:
   ```bash
   docker-compose down
   ```
