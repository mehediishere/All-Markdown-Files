# Laravel Project Installation Guide

This guide will walk you through the process of installing a Laravel project using npm and provide instructions for running it in both local and production environments.

## Prerequisites

Before you begin, ensure you have the following installed:

- PHP
- Composer
- Node.js & npm
- MySQL or any other supported database server

## Step 1: Clone the Repository

Clone the Laravel 10 project repository from GitHub:

```bash
git clone <repository_url>
```

## Step 2: Install PHP Dependencies
Navigate to the project directory and install PHP dependencies using Composer:

```bash
cd <project_directory>
```
```bash
composer install
```

## Step 3: Install Frontend Dependencies
Install frontend dependencies using npm:

```bash
npm install
```

## Step 4: Create Environment File

Duplicate the `.env.example` file and rename it to `.env`. Update the database connection settings and other configuration values as needed.

```bash
cp .env.example .env
```

## Step 5: Generate Application Key
Generate an application key for your Laravel application:

```bash
php artisan key:generate
```

## Step 6: Run Migrations
Run database migrations to create necessary tables:

```bash
php artisan migrate
```

## Step 7: Serve the Application Locally
To run the application locally, use the following command:

```bash
php artisan serve
```

Visit http://localhost:8000 in your web browser to access the application.

## Step 8: Building for Production
Before deploying to a production environment, you should compile frontend assets and optimize the application:

```bash
npm run prod
php artisan config:cache
php artisan route:cache
php artisan view:cache
```

## Step 9: Deploying to Production
Upload the project files to your web server and configure the web server to serve the Laravel application. Ensure the storage and `bootstrap/cache` directories are writable by the web server.

## Step 10: Set Up Environment Variables
Set up environment variables on your production server similar to how you did in the `.env` file for the local environment.

## Step 11: Run Migrations (Optional)
If you haven't already run migrations on the production server, run them now:

```bash
php artisan migrate
```

## Step 12: Serve the Application
After deploying to production, your Laravel application should be accessible via your domain.