# harperdb-digitalocean

## Prerequisites
- [A DigitalOcean account](https://www.digitalocean.com/)
- [Terraform v1.3.7+](https://developer.hashicorp.com/terraform/downloads)

## Digital Ocean (DO) Setup
To give Terraform access, you need a personal access token from DO. Navigate to your API tokens page in the DigitalOcean console. 
Select "Generate New Token."

Copy the token and set the variable in your terminal:
```bash
$ export DIGITALOCEAN_ACCESS_TOKEN=<token-here>
```

## Terraform Setup
- Clone this repository
- Create SSH key: `ssh-keygen -t rsa -C "your_email@example.com" -f ./tf-digitalocean`
- Paste the SSH pubkey to `harperdb.yaml` file
- Create the plan: `terraform plan -out plan.out`
- Create the infra: `terraform apply "plan.out"`

This will create a droplet, set the firewall to allow ssh access and open ports 9925-9926

## Interacting with Harper DB

Send curl commands to create schemas:

```bash
curl --location --request POST <do-public-ip>:9925 \                                                              
  --header 'Content-Type: application/json' \
  --header 'Authorization: Basic SERCX0FETUlOOnBhc3N3b3Jk' \
--data-raw '{
    "operation": "create_schema",
    "schema": "dev"
}'
```
