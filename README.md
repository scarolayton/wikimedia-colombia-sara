# Wikimedia Colombia SARA

A Django web application built with HTMX and Tailwind CSS.

## Tech Stack

- **Django 4.2** - Python web framework
- **HTMX** - Modern frontend interactivity without heavy JavaScript
- **Tailwind CSS** - Utility-first CSS framework
- **django-tailwind** - Tailwind CSS integration for Django
- **django-htmx** - HTMX integration for Django

## Prerequisites

- Python 3.10+
- Node.js 18+ (for Tailwind CSS compilation)
- npm or yarn

## Installation

### 1. Clone the repository

```bash
git clone <repository-url>
cd wikimedia-colombia-sara
```

### 2. Create and activate a virtual environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Python dependencies

```bash
pip install -r requirements.txt
```

### 4. Install Tailwind CSS dependencies

```bash
python manage.py tailwind install
```

### 5. Run database migrations

```bash
python manage.py migrate
```

### 6. Create a superuser (optional)

```bash
python manage.py createsuperuser
```

## Development

You need to run **two terminals** during development:

### Terminal 1: Tailwind CSS compiler

```bash
python manage.py tailwind start
```

This watches for changes in your templates and recompiles the CSS.

### Terminal 2: Django development server

```bash
python manage.py runserver
```

The application will be available at `http://127.0.0.1:8000/`

## Project Structure

```
wikimedia-colombia-sara/
├── core/                   # Main application
│   ├── views.py            # View functions
│   ├── models.py           # Database models
│   └── ...
├── theme/                  # Tailwind CSS app
│   ├── static/
│   │   └── css/
│   │       └── dist/
│   │           └── styles.css  # Compiled CSS (auto-generated)
│   ├── static_src/
│   │   ├── src/
│   │   │   └── styles.css      # Source CSS with Tailwind directives
│   │   ├── tailwind.config.js  # Tailwind configuration
│   │   └── package.json        # Node.js dependencies
│   └── templates/
│       └── base.html           # Base template
├── wikimediacolombiasara/  # Django project settings
│   ├── settings.py
│   ├── urls.py
│   └── ...
├── manage.py
└── requirements.txt
```

## Building for Production

### Compile Tailwind CSS for production

```bash
python manage.py tailwind build
```

This generates a minified CSS file optimized for production.

### Collect static files

```bash
python manage.py collectstatic
```

## Key Configuration

### Tailwind CSS

- Configuration file: `theme/static_src/tailwind.config.js`
- Source CSS: `theme/static_src/src/styles.css`
- Compiled CSS: `theme/static/css/dist/styles.css`

### HTMX

HTMX is included via CDN in the base template. The `django-htmx` middleware provides the `request.htmx` attribute to detect HTMX requests in views:

```python
def my_view(request):
    if request.htmx:
        # Return partial HTML for HTMX request
        return render(request, 'partials/my_partial.html')
    # Return full page for regular request
    return render(request, 'my_page.html')
```

## License

[Add your license here]
