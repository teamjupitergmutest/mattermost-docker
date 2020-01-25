pipeline {
        environment {
            registryCredential = "dockerhub"
            dockerImage = ""
            registry = "teamjupitergmutest/jupiter-test"
        }
        agent any
        stages {
            stage('Build & Publish new Docker images') {
                steps {
                    echo 'Starting to build docker image DB'
                    script {
                        dir ('db') {
                            dockerImage = docker.build(registry + ":db-${BUILD_ID}")
                            docker.withRegistry("https://registry.hub.docker.com", registryCredential){
                            dockerImage.push()
                           }   
                         }
                        }
                    echo 'Starting to build docker image APP'
                    script {
                        dir ('app') {
                            dockerImage = docker.build(registry + ":app-${BUILD_ID}")
                            docker.withRegistry("https://registry.hub.docker.com", registryCredential){
                            dockerImage.push()
                           }   
                         }
                        }
                    echo 'Starting to build docker image WEB'
                    script {
                        dir ('web') {
                            dockerImage = docker.build(registry + ":web-${BUILD_ID}")
                            docker.withRegistry("https://registry.hub.docker.com", registryCredential){
                            dockerImage.push()
                           }   
                         }
                        }
                	}
             	    }
            stage('Remove old Docker images') {
                steps {
                    sh "docker rmi '${registry}:db-${BUILD_ID}'"
                    sh "docker rmi '${registry}:app-${BUILD_ID}'"
                    sh "docker rmi '${registry}:web-${BUILD_ID}'"
                   }
                  }
         }
 }
