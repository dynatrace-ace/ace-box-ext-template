ENVS_FILE = "mac/environments.yaml"

pipeline {
    agent {
        label 'ace'
    }
    environment {
        KUBE_BEARER_TOKEN = credentials('KUBE_BEARER_TOKEN')
        KEPTN_API_TOKEN = credentials('CA_API_TOKEN')
        DT_API_TOKEN = credentials('DT_API_TOKEN')
        DT_TENANT_URL = credentials('DT_TENANT_URL')
    }
    stages {
        stage('Dynatrace base config - Validate') {
			steps {
                container('ace') {
                    script{
                        sh "monaco -v -dry-run -e=$ENVS_FILE -p=infrastructure mac/projects"
                    }
                }
			}
		}
        stage('Dynatrace base config - Deploy') {
			steps {
                container('ace') {
                    script {
				        sh "monaco -v -e=$ENVS_FILE -p=infrastructure mac/projects"
                        sh "sleep 60"
                    }
                }
			}
		}       
        stage('Dynatrace ACE project - Validate') {
			steps {
                container('ace') {
                    script{
                        sh "monaco -v -dry-run -e=$ENVS_FILE -p=ace mac/projects"
                    }
                }
			}
		}
        stage('Dynatrace ACE project - Deploy') {
			steps {
                container('ace') {
                    script {
				        sh "monaco -v -e=$ENVS_FILE -p=ace mac/projects"
                    }
                }
			}
		}       
    }
}