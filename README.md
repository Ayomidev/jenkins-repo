# Jenkins Web App

This is a simple Node.js web application used for Jenkins CI/CD pipeline demonstration.

## Running Locally

1. Install dependencies:

   ```
   npm install
   ```

2. Start the application:

   ```
   npm start
   ```

3. Run tests:

   ```
   npm test
   ```

## Docker

1. Build the Docker image:

   ```
   docker build -t my-web-app-image .
   ```

2. Run the Docker container:

   ```
   docker run -p 8080:8080 my-web-app-image
   ```

3. Access the application at `http://localhost:8080`.

## Jenkins Pipeline

Follow the Jenkinsfile to set up a Jenkins pipeline that builds, tests, and deploys this web application.
