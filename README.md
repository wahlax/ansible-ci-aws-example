# Terraform on AWS with Ansible

This examples uses ansible vault to supply AWS credentials to terraform using an ansible provisioner

```
ansible-playbook -i inventory.ini pipeline.yml -e "ci_work_dir=`pwd`" -e "@vault/secrets.yml" --vault-password-file vault/password-file
```

FILES:

  * `pipeline.yml` - entry point for ansible
  * `pipeline-env.shl` - sets env for terraform
  * `inventory.ini` - defines localhost only right now
  * `main.tf` - aws infra definition in terraform
  * `provisioner.yml` - ansible provisioner used by terraform
  * `requirements.yml` - dependencies of ansible provisioner

NOTES:

 * Ansible provisioner had failed to connect sometimes. Might prefer building inventory from terraform output and provision in next play.
