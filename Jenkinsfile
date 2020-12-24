pipeline {
    agent {
        label "master"
    }
    stages {
        stage('Clone') {
            steps {
                echo "1.Clone Stage"
                git url: "https://github.com/hgcloud/mongo-k8s-sidecar.git"
                script {
                    build_tag = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()
                }
                echo "${build_tag}"
            }
        }
        stage('Test') {
            steps {
                echo "2.Test Stage"
            }
        }
        stage('Build') {
            steps {
                echo "3.Build Docker Image Stage"
            }
        }
        stage('Push') {
            steps {
                echo "4.Push Docker Image Stage"
            }
        }
        stage('YAML') {
            steps {
                echo "5. Change YAML File Stage"
            }
        }
        stage('Deploy') {
            steps {
                echo "6. Deploy Stage"
            }
        }
    }
}
