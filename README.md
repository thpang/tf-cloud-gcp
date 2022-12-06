# tf-cloud-gcp

## Terraform Cloud Usage

When using with Terraform cloud modify the `terraform.auto.tfvars` file and set `tf_enterprise_integration_enabled = true` if it's not.

You also need to set these 2 items in the variables section:

* ssh_public_key - This would be the content of the public side of your id_rsa/id_rsa.pub key pair. This value is set as a `terraform` variable
* GOOGLE_CREDENTIALS - This would be the content of the gcloud subscription json file location in `$HOME/.google` **NOTE**: You must collapse the contents of the file down into a single line. No carige returns or line feeds.

When setting up the workspace you need to specify that the working Terraform directory is `/public` and check to include the submodule near the bottom of the creation dialog.

That should be it.

I know I have my prefix and id info tagged in the tfvars file for now. This can be modified as you need it. No sensitive information is provided in this repo.

## Current Issues

In the tfvars file you must set the `default_public_access_cidrs` value as follows

```yaml
default_public_access_cidrs = ["0.0.0.0/0",]
```
This allows Terraform cloud to create the needed kubernetes entities once the cluster is up to generate the approriate kube config file for cluster access.

In the future this list will include the Terraform Cloud CIDRs needed to allow this without opening the cluster up to the internet.
