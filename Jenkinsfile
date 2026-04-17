pipeline {
  agent any

  options {
    disableConcurrentBuilds()
    timestamps()
  }

  parameters {
    string(
      name: 'IMAGE_TAG',
      defaultValue: 'v1.0.1',
      description: 'Docker image tag to deploy (example: v1.0.1)'
    )
  }

  stages {
    stage('Provision EC2 Instance') {
			steps {
				sh "ansible-playbook playbooks/provision_ec2.yml"
			}
		}
    stage('Deploy Container') {
			steps {
				sh "ansible-playbook playbooks/deploy_container.yml"
			}
		}
  }
}
