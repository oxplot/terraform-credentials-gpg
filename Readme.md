Store your Terraform Cloud API token encrypted by GPG.

## Requirements

- GPG tools
- terraform CLI tool
- A key pair
- Terraform Cloud account with org and a workspace setup

## Getting started

Get a copy of the code:

```
cd ~
git clone https://github.com/oxplot/terraform-credentials-gpg
cd terraform-credentials-gpg
```

Copy or link to `terraform-credentials-gpg` in your terraform plugins
directory:

```
cp terraform-credentials-gpg ~/.terraform.d/plugins/
#ln -s ~/terraform-credentials-gpg/terraform-credentials-gpg ~/.terraform.d/plugins/
```

Configure your terraform to use the GPG credential helper:

```
cat <<EOF >> ~/.terraformrc

credentials_helper "gpg" {
  args = ["1122334455667788", "/home/bobby/.terraform-cloud-token"]
}

EOF
```

*`1122334455667788` is your key ID. Alternatively, you can use the email
address associated with that key.*

*`.terraform-cloud-token` will store gpg encrypted token*

Setup a new terraform project:

```
cd ~
mkdir tf-cloud-test
cd tf-cloud-test
cat <<EOF > backend.tf

terraform {
  backend "remote" {
    organization = "your-org-name"
    workspaces {
      name = "your-workspace"
    }
  }
}

EOF
```

Login to terraform:

```
terraform login
```
