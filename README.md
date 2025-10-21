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
