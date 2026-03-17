# My Docker Tutorial

This project is a simple Node.js and Express application created to demonstrate the basics of containerizing an app with Docker.

## What the Project Does

The application starts a small web server on port `3000` and exposes a single route:

- `GET /` → returns the text `This is Docker tutorial`

The app is intentionally minimal so the focus stays on understanding how Docker packages and runs a Node.js application.

## Project Structure

- `src/server.js` – Express server with one route
- `package.json` – project metadata and dependencies
- `Dockerfile` – instructions for building the Docker image

## How Docker Is Used

The `Dockerfile` does the following:

1. Uses `node:19-alpine` as the base image
2. Copies `package.json` into the container
3. Copies the `src` folder into `/app`
4. Sets `/app` as the working directory
5. Runs `npm install` to install dependencies
6. Exposes port `3000`
7. Starts the server with `node server.js`

Because the contents of `src` are copied directly into `/app`, the file `src/server.js` becomes `/app/server.js` inside the container.

## Run the App Locally

If you want to run the app without Docker:

1. Install dependencies:
   - `npm install`
2. Start the app:
   - `node src/server.js`
3. Open your browser at `http://localhost:3000`

## Build and Run with Docker

### Build the image

- `docker build -t my-docker-tutorial:v1 .`

### Run the container

- `docker run --name my-docker-tutorial -d -p 3000:3000 my-docker-tutorial:v1`

Then open `http://localhost:3000` to see the response.

## Expected Output

When the app is running and you visit the root URL, you should see:

`This is Docker tutorial`

## Purpose of This Repository

This repository is best understood as a beginner-friendly example for learning:

- how to create a small Express server
- how to package a Node.js app with Docker
- how to expose a containerized app on a local port

It is a good starting point for experimenting with Docker commands, image builds, and simple containerized web applications.
