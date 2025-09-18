<div align="center">

# Deepfake Detection using Deep Learning (ResNeXt + LSTM)

by Sarthak Bhamare

</div>

## How to Run

This repository contains a Django web app that detects deepfakes from videos using a ResNeXt backbone and an LSTM classifier.

Prerequisites:
- Python 3.10+ (works on Windows)
- Git
- Optional: Docker (for containerized run)

### A) Run Locally (Recommended)

1) Create and activate a virtual environment

```powershell
python -m venv .venv
.\.venv\Scripts\activate
```

2) Install dependencies

```powershell
pip install --upgrade pip
pip install -r "Django Application/requirements.txt"
```

3) Download/Place model weights

- Put your `.pt` model files into `models/` (this folder is kept but weights are git-ignored). The repo already includes placeholders and some paths in the app expect weights there.

4) Run database migrations (creates local `db.sqlite3`)

```powershell
cd "Django Application"
python manage.py migrate
```

5) Start the server

```powershell
python manage.py runserver
```

6) Open the app

Visit `http://127.0.0.1:8000` in your browser.

Notes:
- Large datasets and uploaded media are ignored by Git. Use the app UI to upload a short test video.
- If you have a CUDA-capable GPU and PyTorch with CUDA installed, the app can leverage it automatically; otherwise it will run on CPU.

### B) Run with Docker (Optional)

1) Build images

```powershell
cd "Django Application"
docker build -t deepfake-app:latest .

cd ..\nginx
docker build -t deepfake-nginx:latest .
```

2) Start containers (example using two terminals or run sequentially)

```powershell
docker run --rm -it -p 8000:8000 deepfake-app:latest
```

Then in another terminal for Nginx (optional):

```powershell
docker run --rm -it -p 80:80 deepfake-nginx:latest
```

Open `http://localhost:80` (Nginx) or `http://localhost:8000` (Django dev server) in your browser.

## License

This project is licensed under the GPLv3. See `LICENSE` for details.
