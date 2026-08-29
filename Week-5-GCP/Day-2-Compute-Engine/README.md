# Day 2 — Learn GCP Compute Engine

## Objective
Learn how to create and manage virtual machines (VMs) on Google Cloud Compute Engine.

## Work Completed
- Explored Compute Engine concepts including machine types, zones, and regions.
- Created the Compute Engine VM used throughout the GCP exercises.
- Connected to and managed the VM using the `gcloud` CLI.
- Practiced starting, stopping, and checking the status of the VM.

## Key Commands
```bash
gcloud compute instances list
gcloud compute instances start gcp-day2-vm --zone=us-east1-b
gcloud compute instances describe gcp-day2-vm --zone=us-east1-b --format="get(status)"
gngcloud compute ssh gcp-day2-vm --zone=us-east1-b
```

## What I Learned
I learned how Compute Engine provides cloud-based virtual machines and how zones, regions, and VM management commands are used to operate cloud infrastructure.
