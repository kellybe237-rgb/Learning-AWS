# Day 5 — Open-Source Project Deployment

## Objective
Clone an open-source Flask application from GitHub and deploy it on a Google Cloud Compute Engine VM.

## Work Completed
- Connected to the Compute Engine VM using the `gcloud` CLI.
- Started the VM and verified that it was running.
- Cloned a Flask application from GitHub.
- Installed the required Flask software and prepared the application.
- Started Flask on `0.0.0.0:5000`.
- Created a GCP firewall rule allowing TCP port `5000` and added the required network tag to the VM.
- Accessed the Flask application successfully through the VM's external IP address in a browser.

## Key Commands
```bash
gcloud compute instances start gcp-day2-vm --zone=us-east1-b
gcloud compute ssh gcp-day2-vm --zone=us-east1-b
git clone https://github.com/mmumshad/simple-webapp-flask.git
cd simple-webapp-flask
sudo apt update
sudo apt install python3-flask -y
export FLASK_APP=app.py
flask run --host=0.0.0.0 --port=5000
```

From the local machine, the VM was configured to allow the Flask port:

```bash
gcloud compute firewall-rules create allow-flask-5000 \
  --network=default \
  --allow=tcp:5000 \
  --source-ranges=0.0.0.0/0 \
  --target-tags=flask

gcloud compute instances add-tags gcp-day2-vm \
  --zone=us-east1-b \
  --tags=flask
```

## What I Learned
I learned how to deploy an open-source application on a cloud VM, configure Flask for external access, and use GCP firewall rules to make an application available through the internet.
