# Flask Docker CI Project

## Project Overview

This project demonstrates how to containerize a simple Flask application using Docker and automate the build process using GitHub Actions.

The main goal of this project was to understand:

* How a backend application runs
* How Docker packages an application into a container
* How CI pipelines automate builds when code is pushed

This project simulates a real DevOps workflow used in modern software teams.

---

# Project Architecture

Developer writes code
↓
Code pushed to GitHub
↓
GitHub Actions CI Pipeline triggers
↓
Docker Image is built automatically

---

# Technologies Used

* Python
* Flask
* Docker
* Git
* GitHub
* GitHub Actions

---

# Project Structure

```
flask-docker-ci/
│
├── app.py
├── requirements.txt
├── Dockerfile
└── .github
     └── workflows
           └── main.yml
```

---

# Step 1 : Flask Application

### app.py

```
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello from Ravindra's Docker Project!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

This is a simple web server built using Flask.

When the root URL `/` is accessed, the server returns a message.

---

# Step 2 : Python Dependencies

### requirements.txt

```
flask
```

This file tells Python which packages need to be installed.

---

# Step 3 : Dockerfile

```
FROM python:3.9

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

EXPOSE 5000

CMD ["python", "app.py"]
```

### Explanation

FROM python:3.9
Base image with Python installed.

WORKDIR /app
Creates the working directory inside the container.

COPY . .
Copies project files into the container.

RUN pip install
Installs required Python packages.

EXPOSE 5000
Opens the Flask server port.

CMD
Runs the Flask application.

---

# Step 4 : Build Docker Image

Docker packages the application and its dependencies into a container image.

Command used:

```
docker build -t flask-docker-app .
```

---

# Step 5 : Run Docker Container

Command:

```
docker run -p 5000:5000 flask-docker-app
```

Now open the browser:

```
http://localhost:5000
```

Output:

```
Hello from Ravindra's Docker Project!
```

---

# Step 6 : CI Pipeline using GitHub Actions

This project uses GitHub Actions to automatically build the Docker image whenever code is pushed to the repository.

Workflow file location:

```
.github/workflows/main.yml
```

### CI Workflow

```
name: Docker CI Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Build Docker Image
        run: docker build -t flask-docker-app .
```

### What happens in CI

1. Code is pushed to GitHub
2. GitHub Actions pipeline starts
3. Runner machine is created
4. Repository code is downloaded
5. Docker image is built automatically

---

# CI Pipeline Output

Example pipeline result:

```
Triggered via push
Status : Success
Total duration : ~21 seconds
```

This means the Docker image was successfully built by the CI pipeline.

---

# What I Learned From This Project

While building this project I learned:

### Application Layer

* How a simple Flask server works
* How APIs return responses

### Containerization

* Why Docker exists
* How applications run inside containers
* How Docker images are built from Dockerfiles

### CI/CD

* How GitHub Actions automates builds
* How CI pipelines run on push events
* How developers verify builds automatically

### DevOps Thinking

* Automating repetitive tasks
* Ensuring code builds consistently
* Creating reproducible environments

---

# Final Output

Local Output:

```
Hello from Ravindra's Docker Project!
```

CI Output:

```
Docker image successfully built in GitHub Actions
```

---

# Future Improvements

Possible next improvements for this project:

* Push Docker image to Docker Hub
* Add automated testing
* Deploy container to cloud server
* Add CD pipeline for automatic deployment


