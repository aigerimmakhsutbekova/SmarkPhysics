
# SmarkPhisics 
# PHP Project with SQLite Database

This documentation provides a step-by-step guide to set up and run a PHP project with an SQLite database. Follow the instructions below to get your project up and running.

## Prerequisites

Before you start, ensure you have the following installed on your system:

- PHP (version 7.4 or higher)
- Composer (for dependency management)
- Git (for version control)
- A web server like Apache or Nginx

## Step 1: Clone the Repository

First, clone the project repository from GitHub to your local machine. Open your terminal and run:

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

Replace `your-username` and `your-repo-name` with your GitHub username and repository name, respectively.

## Step 2: Install Dependencies

Navigate to the project directory and install the PHP dependencies using Composer:

```bash
composer install
```

This command reads the `composer.json` file and installs the dependencies listed.

## Step 3: Set Up the SQLite Database

Create an SQLite database file. You can do this from the terminal:

```bash
touch database/database.sqlite
```

Ensure the directory `database` exists. If it doesn't, create it first:

```bash
mkdir -p database
touch database/database.sqlite
```

## Step 4: Configure Environment Variables

Copy the example environment file to a new `.env` file:

```bash
cp .env.example .env
```

Open the `.env` file in a text editor and update the following lines to configure the SQLite database:

```env
DB_CONNECTION=sqlite
DB_DATABASE=/path/to/your/project/database/database.sqlite
```

Replace `/path/to/your/project` with the absolute path to your project directory.

## Step 5: Run Database Migrations

Run the database migrations to create the necessary tables:

```bash
php artisan migrate
```

This command uses Laravel's migration system to set up the database schema.

## Step 6: Start the Development Server

Start the PHP development server to serve your application:

```bash
php -S localhost:8000 -t public
```

This command serves your project on `http://localhost:8000`.

## Step 7: Access the Application

Open your web browser and navigate to `http://localhost:8000` to see your application in action.

## Additional Configuration (Optional)

### Setting File Permissions

Ensure the `database` directory and `database.sqlite` file have the correct permissions:

```bash
chmod -R 775 database
chmod 664 database/database.sqlite
```

### Setting Up Apache or Nginx

If you prefer using a web server like Apache or Nginx, configure the server to serve your PHP project.

#### Apache Configuration

Create a virtual host for your application:

```apache
<VirtualHost *:80>
    ServerName your-domain.com
    DocumentRoot /path/to/your/project/public

    <Directory /path/to/your/project/public>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/your-project-error.log
    CustomLog ${APACHE_LOG_DIR}/your-project-access.log combined
</VirtualHost>
```

#### Nginx Configuration

Create a server block for your application:

```nginx
server {
    listen 80;
    server_name your-domain.com;

    root /path/to/your/project/public;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```


Happy coding!
