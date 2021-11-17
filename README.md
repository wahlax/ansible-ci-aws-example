# Terraform on AWS with CI built from Ansible

Builds EC2 instance on AWS provisioned by ansible. 2 entry points exist:
  * Jenkinsfile - configured for use with @wahlax/ansible-ci
  * Local ansible pipeline - use ansible-vault for credentials

Example using local ansible pipeline and vault to supply AWS credentials to terraform

```
ansible-playbook -i inventory.ini pipeline.yml -e "ci_work_dir=`pwd`" -e "@vault/secrets.yml" --vault-password-file vault/password-file
```

## Vault Credentials

  * `aws-key-id` - id for aws provisioning
  * `aws-key-secret` - secret for aws provisioning

## Files

  * `Jenkinsfile` - entry point when used with jenkins ci
  * `pipeline.yml` - entry point for ansible (jenkins alternative)
  * `terraform-env.shl` - sets env for terraform
  * `inventory.ini` - defines localhost only right now
  * `main.tf` - aws infra definition in terraform
  * `provisioner.yml` - ansible provisioner used by terraform
  * `requirements.yml` - dependencies of ansible provisioner

## Notes

 * Ansible provisioner had failed to connect sometimes. Might prefer building inventory from terraform output and provision in next play.
