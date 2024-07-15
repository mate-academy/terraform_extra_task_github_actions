# Automated Azure Infrastructure Deployment with Terraform and GitHub Actions

This task demonstrates how to use GitHub Actions to automatically plan and apply Terraform configurations to manage Azure infrastructure.

## Prerequisites

Before you begin, ensure you have the following:

- An Azure subscription
- A GitHub account
- Basic knowledge of Terraform and GitHub Actions.

## Steps to Complete the Task

**1. Fork this Repository**

**2. Azure Setup**

- Create an Azure AD application for authentication. This will be used for GitHub Actions to interact with Azure.
- Create an Azure Storage account for Terraform state. This will store your Terraform state files securely.

**3. GitHub Repository Setup**

- Add the necessary Azure credentials as secrets in your GitHub repository settings. You'll need the `Client ID`, `Subscription ID`, and `Tenant ID`.

**4. Terraform Configuration**

- Update the `main.tf` file with your Azure backend configuration. This should point to the storage account you created.
- Add your Terraform resource configurations to `main.tf`.

**5. Terraform Plan Job**

This job runs on every push to the main branch and on pull requests:

- Checks out the repository
- Sets up Terraform
- Initializes Terraform
- Checks Terraform formatting
- Generates and saves a Terraform plan

**6. Terraform Apply Job**

This job runs only on pushes to the main branch and and on pull requests:

- Checks out the repository
- Sets up Terraform
- Initializes Terraform
- Downloads the saved Terraform plan
- Applies the Terraform plan

**7. Define Workflow Permissions**

- Set the special permissions for OIDC authentication:
    * `id-token: write`: This permission is crucial for OIDC authentication with Azure.
    * `contents: read`: This gives the workflow read access to the repository contents.
    * `pull-requests: write`: This permission allows the workflow to comment on pull requests.

**8. Define Environment Variables for Azure Authentication**

- Set at the workflow level environment variables to authenticate with Azure using OIDC:
    * `ARM_CLIENT_ID`: The Client ID of your Azure AD application.
    * `ARM_SUBSCRIPTION_ID`: Your Azure Subscription ID.
    * `ARM_TENANT_ID`: The Tenant ID of your Azure AD directory.

**9. Test the Workflow**

- Create a new branch for your changes.
- Modify the Terraform configuration files as needed.
- Commit and push your changes.
- Create a pull request to the main branch.

**10. Pull request's description should also contain a reference to a successful workflow run**

