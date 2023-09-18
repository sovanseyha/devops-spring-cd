pipeline {
    agent {
        label 'Node 1'
    }
    stages {
        stage('Update Docker Image') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: 'github-credential', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                            sh "git config user.email yan.sovanseyha@gmail.com"
                            sh "git config user.name sovanseyha"
                            sh "sed -i 's+sovanseyha/devops-spring-test.*+sovanseyha/devops-spring-test:${DOCKERTAG}+g' app/deployment.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done by Jenkins job change manifest: ${env.BUILD_NUMBER}'"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/devops-spring-cd.git HEAD:master"
                        }
                    }
                }
            }
        }
    }
}
