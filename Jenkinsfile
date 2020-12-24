pipeline {
    agent {
        label "master"
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
                   sh(script: 'docker images|grep \'gcr.io/library/cvallance/mongo-k8s-sidecar\'|grep  ${build_tag} > /dev/null 2>&1', returnStdout: true)
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
