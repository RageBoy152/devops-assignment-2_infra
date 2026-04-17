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
				withCredentials([usernamePassword(
					credentialsId: 'dockerhub-credentials',
					usernameVariable: 'DOCKERHUB_USERNAME',
					passwordVariable: 'DOCKERHUB_PASSWORD'
				)]) {
					withEnv([
						"IMAGE_REPOSITORY=rageboy152/devops-assignment-2",
						"IMAGE_TAG=${params.IMAGE_TAG}"
					]) {
						sh "ansible-playbook playbooks/deploy_container.yml"
					}
				}
			}
		}
  }
}
