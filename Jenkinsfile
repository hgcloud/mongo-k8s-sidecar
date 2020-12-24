pipeline {
    agent {
        label "master"
    }
    stages {
        stage('Prepare') {
            steps {
                echo "1.Prepare Stage"
                //git url: "https://github.com/hgcloud/mongo-k8s-sidecar.git"
                //script {
                //    build_tag = sh(returnStdout: true, script: 'git rev-parse --short HEAD').trim()
                //}
                //echo "${build_tag}"
                checkout scm
                script {
                    //echo "build tag: ${build_tag}"
                }
            }
        }
        stage('Test') {
            steps {
                echo "2.Test Stage"
            }
        }
        stage('Build') {
            steps {
                script {
                    echo "3.Build Docker Image Stage"
                    echo "workspace:`pwd`"
                    echo "build tag: ${build_tag}"
                    sh "docker images|grep 'mongo-k8s-sidecar'|grep  ${build_tag} > /dev/null 2>&1"
                    echo $?
                    if ( $? -eq 0 ) {
                        sh "docker rmi gcr.io/library/cvallance/mongo-k8s-sidecar:${build_tag}"
                    }

                    sh "docker build . -t gcr.io/library/cvallance/mongo-k8s-sidecar:${build_tag}"
                    //sh "docker login gcr.io -u admin -p Harbor12345"
                    //sh "docker push gcr.io/library/cvallance/mongo-k8s-sidecar:${build_tag}"
                    //sh "docker rmi gcr.io/library/cvallance/mongo-k8s-sidecar:${build_tag}"
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
