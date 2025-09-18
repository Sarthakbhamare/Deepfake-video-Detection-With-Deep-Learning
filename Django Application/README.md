# Deep fake detection Django Application

## Requirements

Note: A CUDA-capable Nvidia GPU is recommended for best performance (CUDA >= 10.0, Compute Capability > 3.0), but the app can run on CPU.

You can find the list of requirements in [requirements.txt](./requirements.txt). Main requirements are listed below:

```
Python >= 3.8
Django >= 3.0
```

## Directory Structure

- `ml_app` -> Application code (see `views.py`)
- `project_settings` -> Django settings and production configs
- `static` -> CSS, JS, and JSON (face-api)
- `templates` -> HTML templates

Note: Before running the project, ensure directories `models`, `uploaded_images`, and `uploaded_videos` exist at the repo root with proper permissions.

## Run with Docker (optional)

1) Install Docker Desktop and ensure the daemon is running.

2) Build and run the app image from this source:
```
docker build -t deepfake-app:latest .
docker run --rm -it -p 8000:8000 deepfake-app:latest
```

3) (Optional) Build and run nginx proxy from `../nginx`:
```
cd ../nginx
docker build -t deepfake-nginx:latest .
docker run --rm -it -p 80:80 deepfake-nginx:latest
```

Open http://localhost:8000 (Django) or http://localhost:80 (nginx).

## Run locally

1) Create venv and activate (Windows)
```
python -m venv venv
venv\Scripts\activate
```

2) Install requirements
```
pip install -r requirements.txt
```

3) Place model weights in `../models/`

4) Run the development server
```
python manage.py migrate
python manage.py runserver
```

