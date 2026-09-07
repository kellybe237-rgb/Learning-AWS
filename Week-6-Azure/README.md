# Week 6 — Microsoft Azure ☁️

This week focused on Microsoft Azure fundamentals, virtual machines, networking, web application deployment, open-source application deployment, security, monitoring, performance optimization, and resource cleanup.

## Day 1 — Setting Up Azure & Environment Preparation

### Objective
Set up the Azure environment and become familiar with Azure resource management.

### Work completed
- Created and configured an Azure environment.
- Created an Azure resource group for learning exercises.
- Installed and configured the Azure CLI.
- Explored the Azure Portal and Azure resource management concepts.
- Learned the purpose of resource groups and how they help organize cloud resources.

### Key command
```bash
az login
```

## Day 2 — Understanding Core Azure Services

### Objective
Learn the fundamentals of Azure Virtual Machines and Azure Kubernetes Service (AKS).

### Work completed
- Learned how Azure Virtual Machines provide cloud-based compute resources.
- Compared Azure Virtual Machines with AWS EC2.
- Learned the purpose and basic architecture of Azure Kubernetes Service (AKS).
- Created a basic Linux Azure VM through the Azure Portal.
- Connected to the VM successfully using SSH.
- Practiced cleaning up Azure resources after completing the exercise.

## Day 3 — Deploying a Simple Web App on an Azure VM

### Objective
Deploy a web server on an Azure Linux VM and access it from a browser.

### Work completed
- Created the `azure-day3-vm` virtual machine.
- Connected to the VM using an SSH private key.
- Installed Nginx on Ubuntu.
- Verified that the Nginx service was running.
- Configured inbound HTTP access on port `80`.
- Successfully opened the Nginx web page using the VM's public IP address.
- Deleted the Day 3 resource group after completing the exercise.

### Key commands
```bash
chmod 400 "$HOME/Downloads/azure-day3-vm_key.pem"
ssh -i "$HOME/Downloads/azure-day3-vm_key.pem" azureuser@PUBLIC_IP

sudo apt update
sudo apt install nginx -y
sudo systemctl status nginx
curl http://localhost
```

## Day 4 — Working with an Open-Source Project

### Objective
Deploy an open-source Node.js project from GitHub on an Azure VM and troubleshoot application issues.

### Work completed
- Cloned the Azure sample Node.js project from GitHub.
- Installed the project's Node.js dependencies with npm.
- Started the Express.js application.
- Troubleshot a PM2 log permission error.
- Fixed the `/var/log/pm2.log` permission problem.
- Opened port `3000` for the application.
- Successfully accessed the Node.js application through the VM's public IP.
- Deleted the Day 4 resource group after completing the exercise.

### Key commands
```bash
git clone https://github.com/Azure-Samples/js-e2e-vm.git
cd js-e2e-vm
npm install

sudo touch /var/log/pm2.log
sudo chown azureuser:azureuser /var/log/pm2.log
npm start
pm2 list
```

Open application port:

```bash
az vm open-port \
  --resource-group azure-day3-rg \
  --name azure-day3-vm \
  --port 3000 \
  --priority 1010
```

Application test:

```text
http://PUBLIC_IP:3000
```

## Day 5 — Optimization, Security & Documentation

### Objective
Secure the Azure VM, review its performance, optimize resource usage, and document the learning experience.

### Work completed
- Created the `azure-day5-rg` resource group and `azure-day5-vm` virtual machine.
- Checked the VM's hardware profile and current VM size.
- Reviewed available VM sizes in the West US region.
- Used Azure Monitor to review VM performance and CPU utilization.
- Reviewed the Network Security Group (NSG) and verified that only SSH/TCP port `22` was allowed inbound.
- Determined that the VM's very low CPU utilization did not justify increasing its resources.
- Enabled Auto-shutdown to reduce unnecessary VM running costs.
- Deleted the Day 5 resource group after completing the exercise.

### Key commands
Check VM hardware profile:

```bash
az vm show \
  --resource-group azure-day5-rg \
  --name azure-day5-vm \
  --query hardwareProfile \
  --output json
```

List VM sizes:

```bash
az vm list-sizes \
  --location westus \
  --output table
```

Get VM IP addresses:

```bash
az vm list-ip-addresses \
  --resource-group azure-day5-rg \
  --name azure-day5-vm \
  --output table
```

Check the Network Security Group:

```bash
az network nsg list \
  --resource-group azure-day5-rg \
  --output table
```

Check inbound NSG rules:

```bash
az network nsg rule list \
  --resource-group azure-day5-rg \
  --nsg-name azure-day5-vm-nsg \
  --output table
```

The security check confirmed:

```text
SSH | TCP | Inbound | Port 22 | Allow
```

## What new skills, information or understanding have I taken away from this week?

This week, I learned how to set up and manage Microsoft Azure using the Azure Portal and Azure CLI. I gained a better understanding of Azure Virtual Machines, resource groups, networking, and how Azure services compare to AWS. I learned how to create and connect to an Azure VM using SSH keys and manage its resources through the command line. I also deployed a web server and an open-source Node.js application, while learning how to configure firewall rules and troubleshoot application issues. I explored Azure Monitor, checked VM performance, reviewed the VM size, and enabled auto-shutdown to help optimize costs. Finally, I learned how to apply basic Azure security, monitoring, performance optimization, documentation, and resource cleanup practices in a cloud environment.
