# Assignment 2 Infra (Repo B CD Pipeline)

This repo now contains a manual, parameterized Jenkins CD pipeline that:

1. Provisions AWS networking + key material.
2. Provisions a new EC2 instance.
3. Installs Docker, pulls a selected image tag, and runs it on port 80.
4. Performs a final automated health check with `curl` against the instance public IP.

## Jenkins Parameter

- `IMAGE_TAG`: text input for selecting the Docker tag at runtime (only pipeline parameter).

## Hardcoded Pipeline Values

- `IMAGE_REPOSITORY`: `your-dockerhub-user/your-app`
- `AWS_REGION`: `us-east-1`
- `AWS_AMI_ID`: `ami-0866a3c8686eaeeba`
- `EC2_INSTANCE_TYPE`: `t2.micro`
- `EC2_KEY_NAME`: `assignment2_cd_key`
- `AWS_SECURITY_GROUP`: `assignment2_cd_sg`
- `EC2_SSH_USER`: `ubuntu`

EC2 instance name is generated automatically in this format:
`DevOpsAssignment2_Prod-{IMAGE_TAG}-cd-{CD_BUILD}`
where `CD_BUILD` maps to Jenkins `BUILD_NUMBER`.

## Jenkins Credentials Required

- `aws-access-key-id` (Secret text)
- `aws-secret-access-key` (Secret text)
- `dockerhub-credentials` (Username with password)
- `ansible-vault-password` (Secret text)

If your checkout needs GitHub credentials, configure SCM checkout credentials in Jenkins as normal.

## Files Added

- `Jenkinsfile`
- `playbooks/provision_key_security_group.yml`
- `playbooks/provision_ec2.yml`
- `playbooks/deploy_container.yml`

## Vault Handling

The pipeline creates `.artifacts/vault.runtime.yml`, encrypts it with Ansible Vault, and supplies the vault password at execution time from Jenkins credentials.
