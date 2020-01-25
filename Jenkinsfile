
    pipeline {
        environment {
            registryCredential = "dockerhub"
            dockerImage = ""
        }
        agent any
        stages {
            stage('Build Docker images') {
                steps {
                    echo 'Starting to build docker image DB'
                    script {
                        dir ('db') {
                            dockerImage = docker.build("teamjupitergmutest/jupiter-test:db-${BUILD_NUMBER}")
                            docker.withRegistry("https://registry.hub.docker.com", registryCredential){
                            dockerImage.push()
                           }   
                         }
                    echo 'Starting to build docker image APP'
                        dir ('app') {
                            dockerImage = docker.build("teamjupitergmutest/jupiter-test:app-${BUILD_NUMBER}")
                            docker.withRegistry("https://registry.hub.docker.com", registryCredential){
                            dockerImage.push()
                           }
                    echo 'Starting to build docker image WEB'
                        dir ('web') {
                            dockerImage = docker.build("teamjupitergmutest/jupiter-test:web-${BUILD_NUMBER}")
                            docker.withRegistry("https://registry.hub.docker.com", registryCredential){
                            dockerImage.push()
                           }
                    }
                }
            // stage('Additional configurations') {
            //     steps {
            //         sh 'mkdir -pv ./volumes/app/mattermost/{data,logs,config,plugins,client-plugins}'
            //         sh 'chown -R 2000:2000 ./volumes/app/mattermost/'
            //     }
            }
            
        }
    }
