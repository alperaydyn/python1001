<h1>Create Application (local)</h1>
https://cloud.google.com/run/docs/quickstarts/build-and-deploy/deploy-python-service

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
      
```
   vim main.py
``` 
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
```
   Save:  Esc > :w > Enter
   Exit:  Esc > :x > Enter
```
   <li> Create requirements.txt

```
   vim requirements.txt
``` 
```python
   Flask==2.1.0
   gunicorn==20.1.0
``` 
```
   Save:  Esc > :w > Enter
   Exit:  Esc > :x > Enter
```
      
   <li> Create Dockerfile
      
```
   vim Dockerfile
``` 
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
      
```
vim .dockerignore
``` 
```python
Dockerfile
README.md
*.pyc
*.pyo
*.pyd
__pycache__
.pytest_cache
```
     
   <li> Test application </li>
   
```
   python main.py
```
   
   [http://0.0.0.0:8080/](http://0.0.0.0:8080/)

   
</ul>




<h1>Google Cloud (console)</h1>

   https://console.cloud.google.com/


<h2>Create Project</h2>

<h2>Select Project</h2>

  <img width="537" alt="image" src="https://github.com/alperaydyn/python1001/assets/7874545/89bac9d4-0a8e-417d-8d6a-f928f8629e1f">
<h2>New Project</h2>

  <img width="754" alt="image" src="https://github.com/alperaydyn/python1001/assets/7874545/138f5d31-75d2-4bb0-81fd-c6411f4fe0e9">

<h2>Enable Billing</h2>

<h2>Cloud Run</h2>
  - Navigation Menu > [Cloud Run](https://console.cloud.google.com/run)


<h1>Google Cloud (local)</h1>
   <h2>install gcloud</h2>
   https://cloud.google.com/sdk/docs/install-sdk
   <h2>inig gclud</h2>
   https://cloud.google.com/sdk/docs/install-sdk#initializing_the
   
   ```
   gcloud init
   ```
   
   <h2>Login google account (if not logged in before)</h2>
   
   ```
   To continue, you must log in. Would you like to log in (Y/n)? Y
   ```
   
   <h2>Select Project</h2>
   
   ```
   Please enter numeric choice or text value (must exactly match list item):  12
   ```
   <h2>Deploy project</h2>
   
   ```
   gcloud run deploy
   ```   
   ```
   Source code location (Enter)
   ```
   ```
   Service name: python101-v1
   ```
   ```
   Specify region: 17 (europe-west2) 
   ```
   ```
   API [artifactregistry.googleapis.com] not enabled on project [782114615026]. 
   Would you like to enable and retry (this will take a few minutes)? (y/N)?  y
   ```
   
   ```
   Enabling service [artifactregistry.googleapis.com] on project [782114615026]...
   Operation "operations/acat.p2-782114615026-a1a37b38-46f8-4607-8a0e-2737403b579b" finished successfully.
   Deploying from source requires an Artifact Registry Docker repository to store 
   built containers. A repository named [cloud-run-source-deploy] in region 
   [europe-west2] will be created.

   Do you want to continue (Y/n)?  Y   
   ```
   ```
   This command is equivalent to running `gcloud builds submit --tag [IMAGE] /Users/alperaydin/Library/CloudStorage/GoogleDrive-alperaydyn@gmail.com/My Drive/Projects/Python101` and `gcloud run deploy python101-v1 --image [IMAGE]`

   Allow unauthenticated invocations to [python101-v1] (y/N)?  y   
   ```
   ```
   Building using Dockerfile and deploying container to Cloud Run service [python101-v1] in project [python101-386220] region [europe-west2]
   ⠹ Building and deploying new service... Uploading sources.                     
   ⠼ Building and deploying new service... Uploading sources.                     
     ✓ Uploading sources...                                                       
     . Building Container...                                                      
   ⠶ Building and deploying new service... Uploading sources.                     
     . Routing traffic...                                                         
   ✓ Building and deploying new service... Done.                                  
     ✓ Creating Container Repository...                                           u
     ✓ Uploading sources...                                                       
     ✓ Building Container... Logs are available at [https://console.cloud.google.com/cloud-build/builds/e07deafc-420d-4aa5-8688-5167c95a752f?project=782114615026].
     ✓ Creating Revision... Creating Service.                                     
     ✓ Routing traffic...                                                         
     ✓ Setting IAM Policy...                                                      
   Done.                                                                          
   Service [python101-v1] revision [python101-v1-00001-wij] has been deployed and is serving 100 percent of traffic.
   Service URL: https://python101-v1-iietkusjra-nw.a.run.app   
   ```
   
