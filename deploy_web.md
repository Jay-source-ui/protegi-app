# Flutter Web Deployment Guide

This guide explains how to deploy the Protegi Flutter web application to **Firebase Hosting**.

## Prerequisites
- [Firebase CLI](https://firebase.google.com/docs/cli) installed and logged in (`firebase login`).
- Flutter SDK installed and configured.

## Step 1: Build the Web App
Run the following command in the `mobsf_flutter_app` directory to create an optimized production build:

```bash
cd mobsf_flutter_app
flutter build web --release
```

This will generate files in `mobsf_flutter_app/build/web`.

## Step 2: Ensure Firebase is Initialized
The project already has a `firebase.json` in the root. Ensure you are linked to the correct project:

```bash
# In the root 'protegi' directory
firebase use --add
```

## Step 3: Deploy to Hosting
Deploy only the hosting component to avoid affecting other services like Data Connect:

```bash
# In the root 'protegi' directory
firebase deploy --only hosting
```

## Important Considerations for Web
- **CORS**: If your web app fails to fetch data from the backend, ensure the backend's `CORS_ORIGIN` is updated to include your Firebase Hosting URL (e.g., `https://your-project.web.app`).
- **Base URL**: You will need to update the `Server URL` in the app's settings to your production backend URL.
