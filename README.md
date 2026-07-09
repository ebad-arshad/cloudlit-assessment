# Cloudlit DevOps Assessment

Hey there! This is my submission for the Cloudlit DevOps internship assessment. It's a Next.js web application containerized using a multi-stage Docker build to keep the image size super small and production-ready.

## Project Structure
Here's how the repository is laid out:

```
cloudlit-assessment/
├── cloudlit/              # Next.js app source code
│   ├── app/               # App routing and page content
│   ├── public/            # Static assets
│   ├── Dockerfile         # Optimized multi-stage Docker build config
│   ├── package.json       # App dependencies & scripts
│   └── package-lock.json  # NPM lockfile
├── screenshots/           # Screenshots of the working app / build
└── README.md              # This file right here
```

## How to Run

### 1. Locally (Development Mode)
If you want to run it on your machine directly without Docker:

```bash
cd cloudlit
npm install
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) to see the app running.

### 2. With Docker (Production Build)
This is containerized with a 2-stage Docker build to keep things neat and lightweight:

**Build the image:**
```bash
cd cloudlit
docker build -t cloudlit-app .
```

**Run the container:**
```bash
docker run -p 3000:3000 cloudlit-app
```
Once it's running, head over to [http://localhost:3000](http://localhost:3000) in your browser.

## Dockerfile Details (Multi-stage)
* **Stage 1 (Builder):** Uses `node:26-alpine3.23` to install all dependencies (`npm ci`) and build the Next.js app (`npm run build`).
* **Stage 2 (Runner):** Also uses a lightweight Alpine image. It only copies over the compiled `.next` folder, `public` assets, and necessary `node_modules`. It sets up a non-root system user (`nextjs`) for security, exposes port 3000, and starts the server.
