pipeline {
    

    agent any

    stages {
        stage('Checkout Source') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM', 
                        branches: [[name: 'main']],  
                        doGenerateSubmoduleConfigurations: false, 
                        userRemoteConfigs: [[
                            credentialsId: 'github-token', 
                            url: 'https://github.com/aymenzarour/crud-app-k8s-manifest.git'
                        ]]
                    ])
                }
            }
        }

        stage('Update GIT') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github-token', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email aymen.zarour99@gmail.com"
                        sh "git config user.name aymenzarour"
                        //sh "git switch master"
                        sh "cat app-deploy.yaml"
                        sh "sed -i 's+aymenzarour/phpcrudapp.*+aymenzarour/phpcrudapp:${DOCKERTAG}+g' app-deploy.yaml"
                        sh "cat app-deploy.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/crud-app-k8s-manifest.git HEAD:main"
                    }
                }
            }
        }
        
    }
}
