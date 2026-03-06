# Backend Deployment Guide

The `mobsf_backend` is a Python Flask app that acts as a proxy for MobSF. It needs to be hosted on a service that supports persistent execution (unlike a static frontend).

## Recommended Hosting Platforms
- **Google Cloud Run** (Recommended: scales well with Firebase projects)
- **Render**
- **Railway**
- **DigitalOcean App Platform**

## Deployment Steps (General)

### 1. Environment Variables
Your backend needs several environment variables to function correctly in production:

| Variable | Description | Default |
|----------|-------------|---------|
| `MOBSF_URL` | The URL of your running MobSF instance | `http://localhost:8000` |
| `MOBSF_API_KEY` | Your MobSF REST API Key | (Required) |
| `PORT` | The port the server listens on | `5000` |
| `CORS_ORIGIN` | Allowed origin for web requests | `*` (Use your web URL in production) |

### 2. Dockerization
Most modern hosting platforms use Docker. You can use the following `Dockerfile` (create this in `mobsf_backend/Dockerfile`):

```dockerfile
# Use official Python image
FROM python:3.11-slim

# Set working directory
WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Expose port
EXPOSE 5000

# Run the app
CMD ["python", "app.py"]
```

### 3. CI/CD
We recommend setting up a GitHub Action to automatically deploy your backend whenever you push to the `main` branch.

## Connecting the Frontend
After deploying your backend, you will get a URL (e.g., `https://mobsf-backend-abc.a.run.app`). 
1. Open your deployed Protegi Web App.
2. Go to **Settings**.
3. Update the **Server URL** to your new production backend URL.
4. Tap **Test Connection** to verify.
