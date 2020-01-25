
pipeline {
        environment {
            registryCredential = "dockerhub"
            dockerImage = ""
        }
        agent any
        stages {
            stage('Build & Publish new Docker images') {
                steps {
                    echo 'Starting to build docker image DB'
                    script {
                        dir ('db') {
                            dockerImage = docker.build("teamjupitergmutest/jupiter-test:db-${BUILD_NUMBER}")
                            docker.withRegistry("https://registry.hub.docker.com", registryCredential){
                            dockerImage.push()
                           }   
                         }
                        }
                    echo 'Starting to build docker image APP'
                    script {
                        dir ('app') {
                            dockerImage = docker.build("teamjupitergmutest/jupiter-test:app-${BUILD_NUMBER}")
                            docker.withRegistry("https://registry.hub.docker.com", registryCredential){
                            dockerImage.push()
                           }   
                         }
                        }
                    echo 'Starting to build docker image WEB'
                    script {
                        dir ('web') {
                            dockerImage = docker.build("teamjupitergmutest/jupiter-test:web-${BUILD_NUMBER}")
                            docker.withRegistry("https://registry.hub.docker.com", registryCredential){
                            dockerImage.push()
                           }   
                         }
                        }
                	}
             	    }
            stage('Remove old Docker images') {
                steps {
                    echo 'Starting to build docker image DB'
                    echo "${BUILD_NUMBER - 1}"
                    sh "docker rmi teamjupitergmutest/jupiter-test:db-${BUILD_NUMBER-1}"
                    sh "docker rmi teamjupitergmutest/jupiter-test:app-${BUILD_NUMBER-1}"
                    sh "docker rmi teamjupitergmutest/jupiter-test:web-${BUILD_NUMBER-1}"
                   }
                  }
         }
 }
