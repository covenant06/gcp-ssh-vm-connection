# gcp-ssh-vm-connection
### This documentation explains how to provision a virtual machine on Google Cloud Platform (GCP) and connect to it using SSH via MobaXterm, including basic Linux administration commands
🗂 Step 1: Create a Virtual Private Cloud (VPC)

A VPC (Virtual Private Cloud) is a private network where all your cloud resources (like Virtual Machines, Databases, etc.) communicate securely.

✅ Steps:

Go to the GCP Console → VPC Network → Create VPC.

- Enter a name for your VPC (e.g., my-vpc).

- Select the subnet creation mode → choose Custom (so you can manually create subnets).

- Leave default firewall rules unchecked for now (you can add custom ones later).

- Click Create.
# vpc image
<img width="1919" height="917" alt="Screenshot 2025-10-21 092209" src="https://github.com/user-attachments/assets/8b87b9c8-7d0c-4856-932e-f6193dbee8cc" />
🌐 Step 2: Create Subnets

## A subnet is a smaller network inside your VPC. It helps organize and isolate resources within different regions or environments.

✅ Steps:

- Go back to VPC Network → Subnets → Create Subnet.

- Choose your VPC (the one you just created).

- Give your subnet a name (e.g., subnet-a).

- Select a region (for example, us-central1).

- Set an IP address range, like 10.0.1.0/24.

- Click Create.
  <img width="1871" height="877" alt="Screenshot 2025-10-21 092233" src="https://github.com/user-attachments/assets/2470b661-19ad-4ac5-b3e0-ec6c568b0912" />
🔥 Step 3: Configure Firewall Rule for SSH Access

## Before you can connect to your VM using SSH, you need to allow traffic through port 22 — which is the default port for SSH connections.
#### To do this, we’ll create a firewall rule that permits secure access.

✅ Steps:

- In the GCP Console, go to VPC Network → Firewall → Create Firewall Rule.

- Enter a name for your rule (e.g., allow-ssh).

- Under Network, select the VPC you created earlier (e.g., my-vpc).

- In the Targets field, select All instances in the network (or specify a tag if you want limited access).

- Under Source filter, choose IP ranges, and type:
  <img width="1919" height="923" alt="Screenshot 2025-10-21 092314" src="https://github.com/user-attachments/assets/64ca162b-0202-4e01-a1d7-627ce2e07314" />
⚠️ This allows SSH access from anywhere — use only for testing or personal lab setups.
For production environments, limit access to your specific IP range.

Under Protocols and Ports, check Specified protocols and ports → select TCP, then type: 22
Click Create to apply the rule.
## 🧩 Step 4: Creating and Configuring a Service Account

#### A Service Account in Google Cloud is a special type of account used by applications, virtual machines, or services to interact securely with other Google Cloud resources — without needing a user’s credentials.

This ensures secure automation and fine-grained access control across your cloud environment.

✅ Steps:

- In the GCP Console, navigate to:
IAM & Admin → Service Accounts → Create Service Account

- Provide a name and description (e.g., vm-access-service-account).

- Click Create and Continue.

- Assign a role — for example:

-Compute Admin → to manage VM instances

- Service Account User → to allow VM access

- Click Done to finish creating the account.

When creating your VM instance, attach this service account to ensure it inherits the right permissions to access other GCP services.
<img width="1919" height="1076" alt="Screenshot 2025-10-21 092125" src="https://github.com/user-attachments/assets/5d36a7f1-fea9-4f77-9868-ed2eb2984d24" />
✅ Steps:

## creating a vm instance
- Navigate to Compute Engine → VM Instances → Create Instance

- Configure the instance:

- Name: ubuntu-server

- Region & Zone: Same as your subnet (to ensure network connectivity)

- Machine Type: e2-medium (2 vCPU, 4GB RAM)

- Boot Disk: Ubuntu 22.04 LTS (Long Term Support)

- Under Identity and API Access, attach the Service Account you created earlier.
### manually input ssh key inside the vm
  
<img width="1919" height="994" alt="Screenshot 2025-10-20 195125" src="https://github.com/user-attachments/assets/8488b0aa-b012-4f8f-8f1c-e752a81032b4" />

Under Firewall, check:

- ✅ Allow HTTP traffic

- ✅ Allow HTTPS traffic

- Click Create to provision the VM instance.
  
<img width="1908" height="1004" alt="Screenshot 2025-10-21 092025" src="https://github.com/user-attachments/assets/8cb77de2-8575-43a3-9416-00f6c7a9a2b5" />

🧠 Additional Configuration

Generated an SSH key pair from the local terminal using: ssh-keygen -t rsa-b 4096 (this is for generating a very strong passwd)
<img width="1919" height="361" alt="Screenshot 2025-10-21 101912" src="https://github.com/user-attachments/assets/74009ada-2d6e-432d-bb53-f2a82a7c4297" />
### Connected to the VM via MobaXterm (SSH)

<img width="1631" height="942" alt="Screenshot 2025-10-20 211914" src="https://github.com/user-attachments/assets/c499f516-68bc-4844-a088-54cb10a9e07a" />
## Linux Administrative Tasks

After provisioning my VM, I performed some basic Linux administration tasks using the terminal:
i created new users using this command (sudo useradd/adduser name of username)
<img width="1919" height="1079" alt="Screenshot 2025-10-20 214906" src="https://github.com/user-attachments/assets/9491634c-64b9-4340-8820-c796cfa6ec9b" />
Created users and groups for better access management using this commands (sudo groupadd >group name<)
Added users to appropriate groups to follow the principle of least privilege.
<img width="1919" height="1079" alt="Screenshot 2025-10-20 214924" src="https://github.com/user-attachments/assets/e8aaf449-1a2a-4dac-8175-646cf121981f" />
to check activities done; ls -la/
<img width="1916" height="1067" alt="Screenshot 2025-10-20 214750" src="https://github.com/user-attachments/assets/94e44c10-ef7b-4d24-99df-1dd08cc466fe" />
<img width="1919" height="1079" alt="Screenshot 2025-10-20 214843" src="https://github.com/user-attachments/assets/28c48508-b400-4795-8aef-73a05fe5edcc" />
- learnt how to change from root user to admin and i also did other basic linux task I'll be updating with time.
