# Day 3 — Deploy a Simple Web App on GCP

## Objective
Deploy a simple web server on the Compute Engine VM and verify it through the public IP address.

## Work Completed
- SSHed into the Compute Engine VM.
- Installed Nginx on the VM.
- Started and verified the Nginx web server.
- Accessed the VM's public IP address in a web browser to confirm the web server was working.

## Key Commands
```bash
sudo apt update
sudo apt install nginx -y
sudo systemctl status nginx
```

## What I Learned
I learned how to install and manage a web server on a cloud VM and how a public IP address can be used to access an application running on Compute Engine.
