pipeline {
    agent {
        label "nodejs"
    }
    stages {
        stage('Prepare') {
            steps {
                echo "1.Prepare Stage"
                checkout scm
                //script {
                //    build_tag = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()
                //    if (env.BRANCH_NAME != 'master') {
                //        build_tag = "${env.BRANCH_NAME}-${build_tag}"
                //    }
                //}
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
                script {
                   echo "build tag: ${build_tag}"
                   result = sh(script: 'docker images|grep mongo-k8s-sidecar|grep 'v1.0.0'', returnStdout: true)
                   echo "${result}"
                }
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
