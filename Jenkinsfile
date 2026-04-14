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
    stage('Provision Key & Security Group') {
			steps {
				sh "ansible-playbook provision_key_security_group.yml"
			}
		}
    stage('Provision EC2 Instance') {
			steps {
				sh "ansible-playbook provision_container.yml"
			}
		}
  }
}
