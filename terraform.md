# Usage of terraform


## Generate IAM user and policy
- use vscode snippet type `iam_policy` on .tf file


## Terraform to generate aws key and secret
```sh
terraform init
terraform plan -out plan
terraform apply "plan"
terraform output -raw aws_secret_access_key
```