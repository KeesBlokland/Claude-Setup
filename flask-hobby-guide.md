# Flask Project Guide for Hobbyists

## Simple Directory Structure
```
project_root/
├── app/
│   ├── routes/
│   │   ├── main.py        # Main pages
│   │   └── admin.py       # Admin functions
│   ├── templates/
│   │   ├── base.html      # Base template
│   │   └── pages/         # Page templates
│   ├── static/
│   │   ├── css/
│   │   ├── js/
│   │   └── img/
│   └── config.py          # All settings in one place
├── venv/                  # Virtual environment
├── requirements.txt       # Dependencies
└── run.py                # Startup script
```

## Basic File Header Template
```python
"""
main.py
v1.0  2024-12-08
Purpose: Main routes for the website
Changes:
- Added home page
- Added about page
"""
```

## Simple Configuration
```python
# app/config.py
"""
config.py
v1.0  2024-12-08
Purpose: App settings and configuration
"""

class Config:
    # For development, use a simple secret key
    SECRET_KEY = 'dev-key-change-for-production'
    
    # SQLite is perfect for hobby projects
    DATABASE = 'sqlite:///myapp.db'
    
    # Set to False for production
    DEBUG = True

```

## Basic Application Setup
```python
# run.py
"""
run.py
v1.0  2024-12-08
Purpose: Main application startup
"""

from flask import Flask
from app.config import Config

app = Flask(__name__)
app.config.from_object(Config)

# Import routes after app creation
from app.routes import main, admin

if __name__ == '__main__':
    app.run(debug=True)
```

## Simple Routes Organization
```python
# app/routes/main.py
"""
main.py
v1.0  2024-12-08
Purpose: Main website pages
"""

from flask import render_template, Blueprint

main = Blueprint('main', __name__)

@main.route('/')
def home():
    return render_template('pages/home.html')

@main.route('/about')
def about():
    return render_template('pages/about.html')
```

## Basic Error Logging
```python
# Add to run.py
import logging

logging.basicConfig(
    filename='app.log',
    level=logging.INFO,
    format='%(asctime)s - %(message)s'
)

# Example usage in routes
@main.route('/')
def home():
    logging.info('Home page accessed')
    return render_template('pages/home.html')
```

## Environment Settings
```python
# .env
FLASK_DEBUG=True
SECRET_KEY=your-secret-key
```

## Development Tips

1. Keep It Simple:
   - Start small, add features as needed
   - Use SQLite for database (built-in, no setup)
   - Keep routes in one file until you need more

2. Basic Version Control:
   - Use simple version numbers (v1.0, v1.1)
   - Note major changes in file headers
   - Date each change

3. Project Organization:
   - Group related routes together
   - Keep templates in logical folders
   - Use clear, descriptive filenames

4. Helpful Development Practices:
   - Use virtual environment (venv)
   - Keep requirements.txt updated
   - Comment complex code sections
   - Basic error logging
   - Test in development mode

5. Minimum Security:
   - Use secret key
   - Keep .env out of version control
   - Basic input validation
   - Use HTTPS in production

## Getting Started
1. Create virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

2. Install requirements:
```bash
pip install flask
pip freeze > requirements.txt
```

3. Run the app:
```bash
python run.py
```

## Common Templates Structure
```html
<!-- templates/base.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}{% endblock %}</title>
    <link rel="stylesheet" href="{{ url_for('static', filename='css/style.css') }}">
</head>
<body>
    {% block content %}{% endblock %}
</body>
</html>

<!-- templates/pages/home.html -->
{% extends "base.html" %}
{% block title %}Home{% endblock %}
{% block content %}
    <h1>Welcome!</h1>
{% endblock %}
```

Remember: This is a starting point. Add complexity only when you need it. Flask's flexibility means you can grow your project structure as your needs grow.
