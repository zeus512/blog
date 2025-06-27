---
layout: post
title: "Getting Started with Terraform on Google Cloud Platform (GCP)"
author: umesh
categories: [Terraform, Google Cloud Platform, Infrastructure]
tags: [DevOps, Tools, Development]
image: https://media.licdn.com/dms/image/v2/C5612AQF8ctKFwL7g0w/article-cover_image-shrink_423_752/article-cover_image-shrink_423_752/0/1520169579980?e=1756339200&v=beta&t=WFlDG0eI8ldONp1lQOGQKLZ2zFuDVDC11C_xmXH6U84
---

# Building Infrastructure on GCP using Terraform

In this blog, we will walk through the steps required to set up infrastructure on Google Cloud Platform (GCP) using Terraform.

### ✅ Prerequisites

Before we begin, make sure the following tools are installed on your system:

Google Cloud CLI (gcloud)

Check version:

```bash
gcloud --version
```
Terraform v1.2+

Check version:

```bash
terraform --version
```

🛠️ Step-by-Step Setup

### 1. Create a GCP Account and Project

If you haven’t already, create a GCP account.

Create a new project in GCP and note the project ID. This will be used in your Terraform configuration.

### 2. Enable the Compute Engine API

Navigate to APIs & Services → Enable APIs.

Search for Compute Engine API and enable it.

Note: This step must be repeated for each new project you create.

### 3. Authenticate gcloud

After installing the Google Cloud CLI, authenticate using:

```bash
gcloud auth application-default login
```

You’ll receive a URL and be prompted for a verification code.

Login with the same Google account used for your GCP project.

Paste the verification code back in the terminal to complete authentication.

### 4. Set Quota Project (Optional)

To track usage and receive budget warnings, you can set a quota project:

```bash
gcloud auth application-default set-quota-project <PROJECT_ID>
```

Example:

```bash
gcloud auth application-default set-quota-project learn-terraform-gcp-109795
```

## 📄 Writing Your First Terraform Configuration

Create a file named main.tf with the following content:

```bash
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "6.8.0"
    }
  }
}

provider "google" {
  project = "<PROJECT_ID>"
  region  = "us-central1"
  zone    = "us-central1-c"
}

resource "google_compute_network" "vpc_network" {
  name = "terraform-network"
}
```

### 🔍 Breakdown

terraform block specifies the required providers.

hashicorp/google refers to registry.terraform.io/hashicorp/google.

provider block tells Terraform which provider to use and configures it with project ID, region, and zone.

resource block defines the resource to create — in this case, a VPC network.

```bash
Format: resource "<TYPE>" "<NAME>"
```

### ⚙️ Running Terraform Commands

Once your main.tf is ready, run the following commands:

### 1. Initialize the Terraform project

```bash
terraform init
```

This downloads the necessary provider plugins.

### 2. Check Terraform format

```bash
terraform fmt
```
Formats your configuration files according to standard practices.

### 3. Validate the configuration

```bash
terraform validate
```
Ensures your configuration is syntactically valid.

### 4. Apply the configuration

```bash
terraform apply
```
Terraform will show an execution plan, with + signs indicating resources that will be added.

Type yes to confirm.

### 🧾 Verification
Once the apply is complete:

Go to the GCP Console

Navigate to VPC Network under Networking

You should see a new network named terraform-network listed

## 🎉 Conclusion
You’ve now successfully created a VPC network on GCP using Terraform. This setup is the foundation for provisioning more complex infrastructure on Google Cloud. Stay tuned for more!


