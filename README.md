# AI Video Studio — Trend Editor Starter

A responsive Flask starter for an AI-assisted video-editing workflow. It includes user accounts, project saving, eight editing-style presets, a brief-to-editing-blueprint generator, video upload, and an optional FFmpeg transcode export.

## Important reality check
This starter does **not** yet generate full AI-edited videos by itself. The preset engine creates an editing blueprint. The export button currently transcodes the uploaded source video to a compatible MP4; it does not automatically apply all style effects. Real automatic captions, speech transcription, beat detection, generative video, and timeline effect rendering require additional AI/media services and implementation.

## Run on Windows
Open PowerShell in this folder:

```powershell
py --version
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
Copy-Item .env.example .env
.\.venv\Scripts\python.exe app.py
```

Open `http://127.0.0.1:5000`. Create an account, log in, open Studio, choose a preset, and save a project.

If `Copy-Item` says `.env` already exists, that is fine; do not overwrite a secret you have already set.

## FFmpeg (optional)
To enable MP4 export, install FFmpeg from https://ffmpeg.org/download.html and make sure `ffmpeg -version` works in a new terminal. Export in this starter makes a compatible H.264/AAC MP4; it does not yet apply preset-specific effects.

## Where data is stored locally
- Accounts and project metadata: `instance/studio.db`
- Uploaded source videos: `instance/uploads/`
- Exports: `instance/exports/`

Back up the `instance` folder. Deleting it deletes local accounts, projects, uploads, and exports.

## Android and laptop access
The interface is responsive. To test on your Android phone while it shares the same Wi-Fi, run `ipconfig`, find your laptop's IPv4 address, then open `http://YOUR-LAPTOP-IP:5000` on the phone. Allow Python through Windows Firewall if prompted. This is local testing, not public hosting.

## Deploying online
Use a managed database and persistent object storage before production. The local SQLite database and `instance/` folders are not reliable permanent storage on many cloud hosts. Set a strong `SECRET_KEY`, disable debug mode, and configure backups before sharing with other users. A production release should also add CSRF protection, rate limiting, file scanning, and a background job queue for long renders.
