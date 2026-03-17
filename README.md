# Bonton Copilot

A Django 5 REST API project for a travel chatbot application.

## Project Structure

```
BontonCopilotNew/
├── manage.py
├── config/
│   ├── settings/
│   │   ├── __init__.py      # Loads DJANGO_SETTINGS_MODULE or defaults to dev
│   │   ├── base.py          # Shared configuration
│   │   ├── development.py   # Dev-specific overrides
│   │   ├── staging.py       # Staging overrides
│   │   └── production.py    # Production hardening
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
├── apps/                    # Django applications
└── .env.example             # Environment variables template
```

## Quick Start

### Prerequisites

- Python 3.12+
- PostgreSQL
- Redis (optional, for caching)

### Installation

1. Clone the repository and navigate to the project directory:
   ```bash
   cd BontonCopilotNew
   ```

2. Create a virtual environment:
   ```bash
   python -m venv venv
   ```

3. Activate the virtual environment:
   - Windows: `venv\Scripts\activate`
   - macOS/Linux: `source venv/bin/activate`

4. Install Django and required packages:
 ```bash
 pip install django djangorestframework django-cors-headers django-debug-toolbar
 ```

5. Copy the environment template and configure:
   ```bash
   cp .env.example .env
   ```
   Edit `.env` with your specific configuration.

6. Run migrations:
   ```bash
   python manage.py migrate
   ```

7. Start the development server:
   ```bash
   python manage.py runserver
   ```

## Environment Configuration

The project uses split settings based on the `DJANGO_SETTINGS_MODULE` environment variable:

| Environment | Settings Module | Command |
|-------------|----------------|---------|
| Development | `config.settings.development` | `python manage.py runserver` |
| Staging | `config.settings.staging` | `DJANGO_SETTINGS_MODULE=config.settings.staging python manage.py runserver` |
| Production | `config.settings.production` | `DJANGO_SETTINGS_MODULE=config.settings.production python manage.py check --deploy` |

## Environment Variables

See `.env.example` for all available configuration options.

### Required Variables

- `DJANGO_SECRET_KEY` - Django secret key (generate a secure random string)
- `DB_NAME` - PostgreSQL database name
- `DB_USER` - PostgreSQL username
- `DB_PASSWORD` - PostgreSQL password

### Optional Variables

- `DJANGO_SETTINGS_MODULE` - Defaults to `config.settings.development`
- `DB_HOST` - Defaults to `localhost`
- `DB_PORT` - Defaults to `5432`
- `REDIS_URL` - Defaults to `redis://localhost:6379/0`

## Production Deployment

Before deploying to production:

1. Set `DJANGO_SETTINGS_MODULE=config.settings.production`
2. Configure `ALLOWED_HOSTS` with your domain(s)
3. Set `CSRF_TRUSTED_ORIGINS` with your HTTPS origin(s)
4. Run deployment checks:
   ```bash
   python manage.py check --deploy
   ```

## Security

This project implements SOC 2 compliance requirements:
- HTTPS enforcement with HSTS
- Secure session and CSRF cookies
- Secret key management via environment variables
- Production security hardening

## License

Private - All rights reserved.
