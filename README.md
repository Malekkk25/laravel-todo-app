# To-Do List

A task manager built with **Laravel 10**. Users register, log in, and manage their own tasks: create, edit, complete, and delete them. Every action is logged, and users get an email whenever a task is updated. A statistics page shows daily completion rate and average completion time.

## Features

- **Authentication**: register, login, logout, password reset and email verification (Laravel UI scaffolding)
- **Task management (CRUD)**: create, edit and delete tasks with a title and description
- **Task status**: mark tasks as *Completed* or back to *In progress*; completed tasks are highlighted in the list
- **Validation**: title (required, max 255 characters) and description are validated server-side
- **Email notifications**: an email is sent to the user each time a task is updated
- **Activity log**: every create / update / complete / delete action is recorded with [spatie/laravel-activitylog](https://github.com/spatie/laravel-activitylog)
- **Statistics**: daily completion rate and average completion time

## Tech stack

| Layer     | Tools                                   |
|-----------|-----------------------------------------|
| Backend   | PHP 8.1+, Laravel 10                    |
| Database  | MySQL                                   |
| Frontend  | Blade templates, Bootstrap 5, Sass      |
| Build     | Vite                                    |
| Packages  | laravel/ui, laravel/sanctum, spatie/laravel-activitylog |
| Mail      | SMTP (configurable), Mailgun mailer available |

## Getting started

### Prerequisites

- PHP 8.1 or higher
- Composer
- Node.js and npm
- MySQL

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/Malekkk25/To_DO_List.git
cd To_DO_List

# 2. Install dependencies
composer install
npm install

# 3. Set up the environment file
cp .env.example .env
php artisan key:generate
```

### Configure `.env`

Set your database and mail credentials:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=todo_app
DB_USERNAME=root
DB_PASSWORD=your_password

MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=your_email@example.com
MAIL_PASSWORD=your_app_password
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=your_email@example.com
```

> For Gmail, use an [App Password](https://support.google.com/accounts/answer/185833), not your normal password. Never commit real credentials.

### Run the app

```bash
# Create the database tables
php artisan migrate

# Start the frontend build (in one terminal)
npm run dev

# Start the Laravel server (in another terminal)
php artisan serve
```

Open <http://localhost:8000>, register an account and start adding tasks.

## Routes

| Method | URI                         | Description                  |
|--------|-----------------------------|------------------------------|
| GET    | `/task/index`               | List your tasks              |
| GET    | `/tasks/create`             | New task form                |
| POST   | `/tasks/store`              | Save a new task              |
| GET    | `/tasks/{id}/edit`          | Edit task form               |
| PUT    | `/tasks/update`             | Update a task                |
| DELETE | `/tasks/{id}`               | Delete a task                |
| POST   | `/tasks/{task}/complete`    | Mark a task as completed     |
| POST   | `/tasks/{task}/uncomplete`  | Mark a task as in progress   |
| GET    | `/stats/daily`              | Daily statistics             |

## Project structure

```
app/
├── Http/Controllers/
│   ├── ToDoController.php        # Task CRUD and status changes
│   └── StatisticsController.php  # Completion statistics
├── Http/Requests/TaskRequest.php # Validation rules
├── Mail/TaskUpdated.php          # Task update email
└── Models/Task.php
database/migrations/              # tasks, users, activity_log tables
resources/views/                  # Blade views (tasks, auth, emails, layouts)
routes/web.php
```

## Roadmap

- [ ] Weekly and monthly statistics pages
- [ ] Scheduled email reminders / daily report
- [ ] Task due dates and priorities
- [ ] Automated tests

## Author

**Malek** ([@Malekkk25](https://github.com/Malekkk25))

## License

This project is open-sourced under the [MIT license](https://opensource.org/licenses/MIT).
