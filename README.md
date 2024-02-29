# Terraform Google Cloud Platform (GCP) Starter Kit

This repository serves as a starter kit for deploying and managing resources on Google Cloud Platform (GCP) using Terraform. Terraform is a powerful infrastructure as code (IaC) tool that allows you to define and manage your cloud infrastructure in a declarative manner.

## Getting Started

1. **Clone the Repository**: Clone this repository to your local machine using the following command:

   ```bash
   git clone https://github.com/your-username/terraform-gcp-starter.git
   ```
2. **Install Terraform**: If you haven't already, install Terraform on your local machine. You can download Terraform from the [official website](https://www.terraform.io/downloads.html) and follow the installation instructions.
3. **Set Up Google Cloud Credentials**: Before you can deploy resources on GCP, you need to set up your Google Cloud credentials. Follow the [Google Cloud documentation](https://cloud.google.com/docs/authentication/getting-started) to create a service account and download the JSON key file.
4. **Initialize Terraform**: Navigate to the cloned repository directory and run the following command to initialize Terraform:

   ```bash
   terraform init
   ```

## Creating a VM Instance

To create a VM instance without mentioning the network, you can use the following Terraform configuration:

```hcl
resource "google_compute_instance" "terraform" {
  name         = "terraform"
  machine_type = "e2-medium"
  region       = "us-central"
  zone         = "us-central1-a"
  tags         = ["web", "dev"]
}
```

After running `terraform apply`, Terraform will create the VM instance without specifying the network.

## Adding Network and Creating a VM Instance

To add a network and create a VM instance on GCP, you can modify the existing configuration as follows:

```hcl
resource "google_compute_network" "network" {
  name = "my-network"
}

resource "google_compute_instance" "vm_instance" {
  name         = "terraform"
  machine_type = "e2-medium"
  region       = "us-central"
  zone         = "us-central1-a"
  tags         = ["web", "dev"]

  network_interface {
    network = google_compute_network.network.id
  }
}
```

After running `terraform apply`, Terraform will create the network and the VM instance with the specified network.

## Updating the VM Instance

To update the VM instance, you can edit the existing configuration to add tags and change the machine type:

```hcl
resource "google_compute_instance" "vm_instance" {
  name         = "terraform"
  machine_type = "e2-medium"
  region       = "us-central"
  zone         = "us-central1-a"
  tags         = ["web", "dev"]
}
```

After running `terraform apply`, Terraform will update the VM instance with the new tags and machine type.

## Destroying Resources

To destroy the resources created by Terraform, you can run the following command:

```bash
terraform destroy
```

This will remove all the resources created by Terraform, including the VM instance and the network.

## Conclusion

This starter kit provides a basic introduction to deploying and managing resources on GCP using Terraform. It covers creating a VM instance, adding a network, updating the VM instance, and destroying resources. For more advanced use cases and configurations, refer to the [Terraform documentation](https://www.terraform.io/docs/index.html) and the [Google Cloud documentation](https://cloud.google.com/docs).

Happy Terraforming!
