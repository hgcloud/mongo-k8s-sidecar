pipeline {
    agent {
        label "nodejs"
    }
    stages {
        stage('Prepare') {
            steps {
                echo "1.Prepare Stage"
                //checkout scm
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
                   result = sh(script: 'docker images|grep gcr.io/library/cvallance/mongo-k8s-sidecar|grep "${build_tag}"', returnStatus: true)
                   if ( result == 0 ) {
                       sh(script: "docker rmi gcr.io/library/cvallance/mongo-k8s-sidecar:${build_tag}", returnStdout: true)
                   }
                   sh(script: "docker build . -t gcr.io/library/cvallance/mongo-k8s-sidecar:${build_tag}", returnStdout: true)
                }
            }
        }
        stage('Push') {
            steps {
                echo "4.Push Docker Image Stage"
                withCredentials([usernamePassword(credentialsId: 'gcrRegistry', passwordVariable: 'gcrRegistryPassword', usernameVariable: 'gcrRegistryUser')]) {
                    sh(script: "docker login -u ${gcrRegistryUser} -p ${gcrRegistryPassword} gcr.io", returnStdout: true)
                    sh(script: "docker push gcr.io/library/cvallance/mongo-k8s-sidecar:${build_tag}", returnStdout: true)
                }
                sh(script: "docker rmi gcr.io/library/cvallance/mongo-k8s-sidecar:${build_tag}", returnStdout: true)
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
