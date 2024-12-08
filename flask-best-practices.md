# Flask Project Best Practices Guide

## Directory Structure
```
project_root/
├── app/
│   ├── __init__.py
│   ├── routes/
│   │   ├── __init__.py
│   │   ├── rt_main.py
│   │   ├── rt_auth.py
│   │   └── rt_api.py
│   ├── models/
│   │   ├── __init__.py
│   │   └── md_user.py
│   ├── templates/
│   │   ├── base.html
│   │   └── tpl_dashboard.html
│   ├── static/
│   │   ├── css/
│   │   ├── js/
│   │   └── img/
│   └── utils/
│       ├── __init__.py
│       └── ut_helpers.py
├── config/
│   ├── __init__.py
│   ├── cfg_development.py
│   ├── cfg_production.py
│   └── cfg_testing.py
├── tests/
│   ├── __init__.py
│   └── test_routes/
│       └── tst_main.py
├── logs/
├── venv/
├── requirements.txt
├── run.py
└── README.md
```

## Naming Conventions

1. File Naming
   - Use lowercase with underscores
   - Prefix files with abbreviated directory name:
     - Routes: `rt_`
     - Models: `md_`
     - Templates: `tpl_`
     - Config: `cfg_`
     - Utils: `ut_`
     - Tests: `tst_`

2. Function/Variable Naming
   - Routes: `route_purpose_action()`
   - Models: `ModelName`
   - Utils: `utility_purpose()`

## Configuration Management

1. Config File Structure:
```python
# config/cfg_base.py
class BaseConfig:
    SECRET_KEY = 'your-secret-key'
    SQLALCHEMY_TRACK_MODIFICATIONS = False

# config/cfg_development.py
from .cfg_base import BaseConfig

class DevelopmentConfig(BaseConfig):
    DEBUG = True
    SQLALCHEMY_DATABASE_URI = 'sqlite:///dev.db'
    
# config/cfg_production.py
from .cfg_base import BaseConfig

class ProductionConfig(BaseConfig):
    DEBUG = False
    SQLALCHEMY_DATABASE_URI = 'postgresql://user:pass@localhost/db'
```

## Application Factory Pattern

```python
# app/__init__.py
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate
from config.cfg_development import DevelopmentConfig

db = SQLAlchemy()
migrate = Migrate()

def create_app(config_class=DevelopmentConfig):
    app = Flask(__name__)
    app.config.from_object(config_class)

    db.init_app(app)
    migrate.init_app(app, db)

    from app.routes import rt_main, rt_auth, rt_api
    app.register_blueprint(rt_main.bp)
    app.register_blueprint(rt_auth.bp)
    app.register_blueprint(rt_api.bp)

    return app
```

## Blueprint Organization

```python
# app/routes/rt_main.py
from flask import Blueprint, render_template

bp = Blueprint('main', __name__)

@bp.route('/')
def route_main_index():
    return render_template('tpl_dashboard.html')
```

## Environment Variables
```bash
# .env
FLASK_APP=run.py
FLASK_ENV=development
DATABASE_URL=postgresql://user:pass@localhost/db
SECRET_KEY=your-secret-key
```

## Logging Configuration
```python
# app/utils/ut_logger.py
import logging
from logging.handlers import RotatingFileHandler
import os

def setup_logger(app):
    if not os.path.exists('logs'):
        os.mkdir('logs')
    
    file_handler = RotatingFileHandler(
        'logs/app.log', 
        maxBytes=10240, 
        backupCount=10
    )
    
    formatter = logging.Formatter(
        '%(asctime)s %(levelname)s: %(message)s '
        '[in %(pathname)s:%(lineno)d]'
    )
    
    file_handler.setFormatter(formatter)
    app.logger.addHandler(file_handler)
    app.logger.setLevel(logging.INFO)
```

## Best Practices Summary

1. Directory Structure:
   - Separate concerns into distinct directories
   - Use blueprints for route organization
   - Keep configuration files isolated
   - Maintain clear separation of static assets

2. Configuration:
   - Use environment-specific config files
   - Store sensitive data in environment variables
   - Implement configuration classes
   - Use application factory pattern

3. Development:
   - Implement proper logging
   - Use blueprints for route organization
   - Follow consistent naming conventions
   - Keep requirements updated
   - Implement proper error handling
   - Use virtual environments

4. Security:
   - Store secrets in environment variables
   - Use configuration classes for sensitive data
   - Implement proper session handling
   - Use secure headers
   - Implement CSRF protection

5. Testing:
   - Maintain separate test configurations
   - Organize tests to mirror application structure
   - Use proper test naming conventions
   - Implement continuous integration
