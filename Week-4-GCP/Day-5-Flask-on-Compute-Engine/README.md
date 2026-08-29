# Day 5 — Open-Source Project Deployment 🚀

## Objective

- Clone a simple open-source Flask application from GitHub.
- Deploy the Flask application on the Google Cloud Compute Engine VM created earlier.
- Configure network access and verify the application in a browser.

## Work completed

I connected to the Google Cloud Compute Engine VM using the `gcloud` CLI. The VM was initially stopped, so I started it before connecting. I cloned a simple open-source Flask application from GitHub, installed Flask, ran the application on port `5000`, configured a GCP firewall rule, and successfully accessed the application through a web browser.

## Start the VM

```bash
gcloud compute instances start gcp-day2-vm \
  --zone=us-east1-b
```

## Connect to the VM

```bash
gcloud compute ssh gcp-day2-vm \
  --zone=us-east1-b
```

## Clone the Flask application

```bash
git clone https://github.com/mmumshad/simple-webapp-flask.git
cd simple-webapp-flask
```

Check the files:

```bash
ls
```

## Install Flask

```bash
sudo apt update
sudo apt install python3-flask -y
```

Set the application:

```bash
export FLASK_APP=app.py
```

## Run the application

```bash
flask run --host=0.0.0.0 --port=5000
```

## Configure the GCP firewall

```bash
gcloud compute firewall-rules create allow-flask-5000 \
  --network=default \
  --allow=tcp:5000 \
  --source-ranges=0.0.0.0/0 \
  --target-tags=flask
```

Add the matching tag to the VM:

```bash
gcloud compute instances add-tags gcp-day2-vm \
  --zone=us-east1-b \
  --tags=flask
```

## Get the external IP

```bash
gcloud compute instances describe gcp-day2-vm \
  --zone=us-east1-b \
  --format="get(networkInterfaces[0].accessConfigs[0].natIP)"
```

The application was accessed in the browser using:

```text
http://EXTERNAL_IP:5000
```

## Result

The Flask application was successfully deployed on the Compute Engine VM and accessed from a web browser through the VM's external IP address and port `5000`.

## Key skills

- Compute Engine
- Linux VM management
- Git and GitHub
- Flask deployment
- Python application hosting
- GCP firewall rules
- External IP addresses
- Network ports
- Cloud application troubleshooting
