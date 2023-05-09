<ul>
   <li>Create/Navigate project directory 

```
   cd /Users/alperaydin/Google\ Drive/My\ Drive/Projects/Python101
```
   <li> Create directory 
      
```
   mkdir app
```
   <li> Create main.py
      
```python
import os
from flask import Flask
      
app = Flask(__name__)

@app.route("/")
def hello_world():
    return "Hello World!"

if __name__ == "__main__":
    app.run(debug=True, host="0.0.0.0", port=int(os.environ.get("PORT", 8080)))   
```
      
   <li> Create requirements.txt

```python
Flask==2.1.0
gunicorn==20.1.0
``` 
   
   <li> Create Dockerfile
      
```python
# Use the official lightweight Python image.
# https://hub.docker.com/_/python
FROM python:3.11-slim

# Allow statements and log messages to immediately appear in the Knative logs
ENV PYTHONUNBUFFERED True

# Copy local code to the container image.
ENV APP_HOME /app
WORKDIR $APP_HOME
COPY . ./

# Install production dependencies.
RUN pip install --no-cache-dir -r requirements.txt

# Run the web service on container startup. Here we use the gunicorn
# webserver, with one worker process and 8 threads.
# For environments with multiple CPU cores, increase the number of workers
# to be equal to the cores available.
# Timeout is set to 0 to disable the timeouts of the workers to allow Cloud Run to handle instance scaling.
CMD exec gunicorn --bind :$PORT --workers 1 --threads 8 --timeout 0 main:app
```
      
   <li> Create .dockerignore file
```python
Dockerfile
README.md
*.pyc
*.pyo
*.pyd
__pycache__
.pytest_cache
```
     
</ul>

<h1>Google Cloud</h1>

   https://console.cloud.google.com/


<h1>Create Project</h1>

<h2>Select Project</h2>

  <img width="537" alt="image" src="https://github.com/alperaydyn/python1001/assets/7874545/89bac9d4-0a8e-417d-8d6a-f928f8629e1f">
<h2>New Project</h2>

  <img width="754" alt="image" src="https://github.com/alperaydyn/python1001/assets/7874545/138f5d31-75d2-4bb0-81fd-c6411f4fe0e9">

<h1>Enable Billing</h1>

<h1>Cloud Run</h1>
  - Navigation Menu > [Cloud Run](https://console.cloud.google.com/run)

<h1>Create Application (local)</h1>
https://cloud.google.com/run/docs/quickstarts/build-and-deploy/deploy-python-service

<ul>
   <li> 
   <li> 
</ul>

