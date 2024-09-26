// pipeline {
//     agent any
    
//     environment {
//         DOCKERHUB_ID = 'surabhiharsha5'
//     }
//     stages {
//         stage('Clone repository') {
//             steps {
//                 git(
//                     url: 'https://github.com/Sri-Harsha-S/Helm-Chart-Practice-K8S.git',
//                     branch: 'master',
//                     credentialsId: 'GITHUB_TOKEN'
//                 )
//             }
//         }

//         stage('Update GIT') {
//             steps {
//                 script {
//                     catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
//                         withCredentials([usernamePassword(credentialsId: 'GITHUB_PSWD', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
//                             withCredentials([usernamePassword(credentialsId: 'DOCKERHUB_ID_PWD', usernameVariable: 'DOCKERHUB_ID', passwordVariable: 'DOCKERHUB_PWD')]){
                                    
    //                                 sh "git config --global user.email 'srisurabhi5@example.com'"
    //                                 sh "git config --global user.name 'Sri-Harsha-S'"
    
                                        // sh "docker tag $DOCKERTAG $IMG_TAG"
    //                                 // Update the version tags under each service in the prod-values.yaml
    //                                 sh "sed -i '/apigateway:/,/version:/ s/version: .*/version: ${DOCKERHUB_ID}/' prod-values.yaml"
    //                                 sh "sed -i '/customersservice:/,/version:/ s/version: .*/version: ${DOCKERHUB_ID}/' prod-values.yaml"
    //                                 sh "sed -i '/vetsservice:/,/version:/ s/version: .*/version: ${DOCKERHUB_ID}/' prod-values.yaml"
    //                                 sh "sed -i '/visitsservice:/,/version:/ s/version: .*/version: ${DOCKERHUB_ID}/' prod-values.yaml"
    
    //                                 sh "cat prod-values.yaml"
    
    //                                 sh "#############################"
    //                                 // Commit and push changes
    //                                 sh "git add ."
    //                                 sh "git commit -m 'Jenkins Job Update: ${env.BUILD_NUMBER} - Deployed new version of petclinic using images with tag ${DOCKERTAG}'"
    //                                 sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Helm-Chart-Practice-K8S.git HEAD:master"
//                             }
//                         }
//                     }
//                 }
//             }
//         }
//     }
// }

// pipeline {
//     agent any
    
//     parameters {
//         string(name: 'DOCKERHUB_ID', defaultValue: 'your-dockerhub-id', description: 'Your Docker Hub ID')
//     }
//     stages {
//         stage('Clone repository') {
//             steps {
//                 git(
//                     url: 'https://github.com/Sri-Harsha-S/Helm-Chart-Practice-K8S',
//                     branch: 'master',
//                     credentialsId: 'GITHUB_PSWD'
//                 )
//             }
//         }

//         stage('Update GIT') {
//             steps {
//                 script {
//                     catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
//                         withCredentials([usernamePassword(credentialsId: 'GITHUB_PSWD', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
//                             sh "git config --global user.email srisurabhi5@example.com"
//                             sh "git config --global user.name Sri-Harsha-S"
        
//                             sh "sed -i '/apigateway:/,/version:/ s/version: .*/version: ${DOCKERHUB_ID}/' prod-values.yaml"
//                             sh "sed -i '/customersservice:/,/version:/ s/version: .*/version: ${DOCKERHUB_ID}/' prod-values.yaml"
//                             sh "sed -i '/vetsservice:/,/version:/ s/version: .*/version: ${DOCKERHUB_ID}/' prod-values.yaml"
//                             sh "sed -i '/visitsservice:/,/version:/ s/version: .*/version: ${DOCKERHUB_ID}/' prod-values.yaml"
//                             sh "cat prod-values.yaml"
//                             sh "git add ."
//                             sh "git commit -m 'Jenkins Job Update: ${env.BUILD_NUMBER} - Deployed new version of petclinic using images with tag ${DOCKERHUB_ID}'"
//                             sh "git push origin master"
//                         }
//                     }
//                 }
//             }
//         }
//     }
// }

pipeline {
    agent any
    environment {
        // AWS_REGION = "eu-west-3"
        // AWS_ACCESS_KEY_ID = credentials('ACCESS_KEY_AWS')
        // AWS_SECRET_ACCESS_KEY = credentials('SECRET_KEY_AWS')
        ECR_REGISTRY = "565393062704.dkr.ecr.eu-west-3.amazonaws.com"
    }
    stages {
        stage('Clean WorkSpace') {
            steps {
                deleteDir()
            }
        }
        stage('Checkout') {
            steps {
                git 'https://github.com/Sri-Harsha-S/Helm-Chart-Practice-K8S.git'
            }
        }
        stage('Build and Push') {
            steps {
                script {
                    sh 'ls -l'
                    withCredentials([usernamePassword(credentialsId: 'DOCKERHUB_ID_PWD', usernameVariable: 'DOCKERHUB_ID', passwordVariable: 'DOCKERHUB_PWD')]){
                        sh 'docker login -u $DOCKERHUB_ID -p $DOCKERHUB_PWD'
                        
                        sh "sed -i '/apigateway:/,/version:/ s/version: .*/version: ${IMAGEVERSION}/' prod-values.yaml"
                        sh "sed -i '/customersservice:/,/version:/ s/version: .*/version: ${IMAGEVERSION}/' prod-values.yaml"
                        sh "sed -i '/vetsservice:/,/version:/ s/version: .*/version: ${IMAGEVERSION}/' prod-values.yaml"
                        sh "sed -i '/visitsservice:/,/version:/ s/version: .*/version: ${IMAGEVERSION}/' prod-values.yaml"

                        // sh "sed -i '/apigateway:/,/image:/ s/image: .*/image: ${ECR_REGISTRY}/' prod-values.yaml"
                        // sh "sed -i '/customersservice:/,/image:/ s/image: .*/image: ${ECR_REGISTRY}/' prod-values.yaml"
                        // sh "sed -i '/vetsservice:/,/image:/ s/image: .*/image: ${ECR_REGISTRY}/' prod-values.yaml"
                        // sh "sed -i '/visitsservice:/,/image:/ s/image: .*/image: ${ECR_REGISTRY}/' prod-values.yaml"
                        
                        sh "cat prod-values.yaml"
                    }
                }
            }
        }
        
        stage('Commit Changes to GitHub') {
            steps {
                script {
                    sh "git config --global user.email 'srisurabhi5@example.com'"
                    sh "git config --global user.name 'Sri-Harsha-S'"
                    def status = sh(script: 'git status --porcelain', returnStdout: true).trim()
                    if (status) {
                        withCredentials([string(credentialsId: 'GITHUB_TOKEN', variable: 'GITHUB_PAT')]){
                        sh """
                           git add .
                           git commit -m "Update image tag to ${IMAGEVERSION}"
                           git push https://Sri-Harsha-S:${GITHUB_PAT}@github.com/Sri-Harsha-S/Helm-Chart-Practice-K8S.git master
                        """
                        }
                    }else {
                        echo "No changes to commit."
                        }
                    }
                }
            }
        }
    }
