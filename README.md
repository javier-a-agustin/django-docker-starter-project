# Django Docker Starter Project

A containerized Django development environment with PostgreSQL/MySQL support using Docker Compose.

## 🚀 Quick Start

```bash
# Clone the repository
git clone <repository-url>
cd django-docker-starter-project

# Start the application
docker-compose up -d

# Access the application
# Django: http://localhost:8000
# PostgreSQL: localhost:5432
```

## 📁 Project Structure

```
django-docker-starter-project/
├── app/                    # Django application
│   ├── app/               # Django project settings
│   │   ├── settings.py    # Django configuration
│   │   ├── urls.py        # URL routing
│   │   ├── wsgi.py        # WSGI configuration
│   │   └── asgi.py        # ASGI configuration
│   ├── manage.py          # Django management script
│   └── requirements.txt   # Python dependencies
├── dockerfiles/           # Docker configurations
│   └── DockerfileDjango   # Django container definition
├── env_variables/         # Environment configurations
│   ├── django.env         # Django environment variables
│   ├── postgres.env       # PostgreSQL configuration
│   └── mysql.env          # MySQL configuration (optional)
├── docker-compose.yml     # Multi-container orchestration
├── up.sh                  # Quick start script
└── .env                   # Docker Compose environment variables
```

## 🛠 Technology Stack

- **Framework:** Django 5.2.5
- **Database:** PostgreSQL 17.6 (default) / MySQL 8.0 (optional)
- **API:** Django REST Framework 3.16.1
- **Container:** Docker & Docker Compose
- **Python:** 3.12

## 📦 Dependencies

### Python Packages
- `psycopg2-binary==2.9.9` - PostgreSQL adapter
- `Django==5.2.5` - Web framework
- `djangorestframework==3.16.1` - REST API framework
- `drf-yasg==1.21.10` - API documentation

### Optional
- `mysqlclient==2.2.7` - MySQL adapter (commented out)

## ⚙️ Configuration

### Environment Variables

The project uses environment files in `env_variables/` directory:

- **django.env**: Django-specific settings
- **postgres.env**: PostgreSQL database credentials
- **mysql.env**: MySQL database credentials (if using MySQL)

### Network Configuration

The project uses a configurable Docker network. Set the network name via environment variable:

```bash
# In .env file
NETWORK_NAME=my-custom-network

# Or export in shell
export NETWORK_NAME=my-custom-network
```

Default network name: `starter-project`

## 🗄 Database Options

### PostgreSQL (Default)
The project is configured to use PostgreSQL 17.6 by default.

### MySQL (Alternative)
To switch to MySQL:
1. Uncomment the MySQL service in `docker-compose.yml`
2. Comment out the PostgreSQL service
3. Update the database configuration in `env_variables/django.env`
4. Uncomment `mysqlclient` in `requirements.txt`

## 🚀 Usage Commands

```bash
# Start all services
docker-compose up -d

# Start only Django (requires database to be running)
./up.sh

# View logs
docker-compose logs -f django
docker-compose logs -f postgres

# Stop services
docker-compose down

# Rebuild containers
docker-compose build --no-cache

# Django management commands
docker-compose exec django python manage.py migrate
docker-compose exec django python manage.py createsuperuser
docker-compose exec django python manage.py collectstatic
```

## 🔧 Development

### Adding New Django Apps
```bash
docker-compose exec django python manage.py startapp myapp
```

### Database Migrations
```bash
docker-compose exec django python manage.py makemigrations
docker-compose exec django python manage.py migrate
```

### Installing New Dependencies
1. Add package to `app/requirements.txt`
2. Rebuild the Django container:
   ```bash
   docker-compose build django
   docker-compose up -d
   ```

## 📝 API Documentation

The project includes drf-yasg for automatic API documentation. Once running, visit:
- Swagger UI: http://localhost:8000/swagger/
- ReDoc: http://localhost:8000/redoc/

## ⚠️ Important Notes

- **Development Only**: This configuration is **NOT production-ready**
- **Security**: Default settings include DEBUG=True and a hardcoded SECRET_KEY
- **Persistence**: Database data is stored in `./data/db/` directory
- **Network**: Requires external Docker network (created automatically or manually)

## 🛡 Production Considerations

Before deploying to production:
- [ ] Change SECRET_KEY to a secure, random value
- [ ] Set DEBUG=False
- [ ] Configure ALLOWED_HOSTS appropriately
- [ ] Use environment variables for sensitive data
- [ ] Set up proper SSL/HTTPS
- [ ] Configure logging
- [ ] Use production-grade database settings
- [ ] Implement proper backup strategies

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

---

**Note**: This is a development starter template. Always review and modify configurations before using in production environments.