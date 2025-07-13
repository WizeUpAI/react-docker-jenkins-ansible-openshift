pipeline {
    agent any

    environment {
        IMAGE_NAME = 'your-dockerhub-user/react-app'
        VERSION = "1.0.${BUILD_NUMBER}"
        DOCKER_CREDENTIALS_ID = 'docker-hub-creds'
        ANSIBLE_PLAYBOOK = 'ansible/deploy-react-openshift.yml'
        OC_PROJECT = 'react-app'
        REACT_BUILD_DIR = 'build'
    }

    tools {
        nodejs 'Node 18'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/your-org/react-openshift-deploy.git', branch: 'main'
            }
        }

        stage('Install & Build React App') {
            steps {
                sh '''
                npm install
                npm run build
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${VERSION}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', DOCKER_CREDENTIALS_ID) {
                        docker.image("${IMAGE_NAME}:${VERSION}").push()
                    }
                }
            }
        }

        stage('Deploy to OpenShift with Ansible') {
            steps {
                sh "ansible-playbook ${ANSIBLE_PLAYBOOK} -e image_name=${IMAGE_NAME} -e image_tag=${VERSION} -e project=${OC_PROJECT}"
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful!"
        }
        failure {
            echo "❌ Deployment failed."
        }
    }
}