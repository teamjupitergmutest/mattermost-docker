
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
                            dockerImage = docker.build("mattermost-docker_db:${BUILD_NUMBER}")
                            docker.withRegistry("https://hub.docker.com/repository/docker/teamjupitergmutest/jupiter-test", registryCredential){
                            dockerImage.push()
                           }   
                         }
                    echo 'Starting to build docker image APP'
                        dir ('app') {
                              sh 'docker build -t mattermost-docker_app:${BUILD_NUMBER} .'
                              sh 'docker tag mattermost-docker_app:${BUILD_NUMBER} teamjupitergmutest/jupiter-test'
                              sh 'docker push teamjupitergmutest/jupiter-test'
                           }
                    echo 'Starting to build docker image WEB'
                        dir ('app') {
                              sh 'docker build -t mattermost-docker_web:${BUILD_NUMBER} .'
                              sh 'docker tag mattermost-docker_web:${BUILD_NUMBER} teamjupitergmutest/jupiter-test'
                              sh 'docker push teamjupitergmutest/jupiter-test'
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
