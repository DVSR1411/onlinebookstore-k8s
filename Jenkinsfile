pipeline {
    agent any
    tools {
        git 'Default'
    }
    stages {
        stage('Update manifest') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'git', passwordVariable: 'passwd', usernameVariable: 'user')]) {
                    sh "git config user.name $user"
                    sh "git config user.email satwikreddy.danda@hotmail.com"
                    git "https://github.com/${user}/onlinebookstore-k8s.git" 
                    sh "sed -i 's+dvsr1411/onlinebookstore.*+dvsr1411/onlinebookstore:$params.dockertag+g' tomcat.yml"
                    sh "git add ."
                    sh "git commit -m Commit-$params.dockertag"
                    sh "git push https://$user:$passwd@github.com/$user/onlinebookstore-k8s.git master"
                }
            }
        }
    }
}
