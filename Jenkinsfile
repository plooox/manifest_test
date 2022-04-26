pipeline {
    agent any
    stages {
        stage('K8S Manifest Update') {
            steps {
                git credentialsId: '4b1dcb95-da80-40e8-8a26-312fb71aed5a',
                    url: 'https://github.com/plooox/manifest_test.git',
                    branch: 'master'
                sh "echo 1"
                sh "cd ./dev && sed -i 's/newTag:.*\$/newTag:${BUILD_NUMBER}/g' kustomization.yaml"
                sh "cat ./dev/kustomization.yaml"
                sh 'git config --global user.name plooox'
                sh 'git config --global user.email insukim97@gmail.com'
                sh "git add ."
                sh "git commit -m '[UPDATE] modoosugang_server ${BUILD_NUMBER} image versioning'"
                sshagent(credentials: ['5bf01c16-c17c-4ec8-a328-a94174ee9b38']) {
                    sh "git remote set-url origin git@github.com:plooox/manifest_test.git"
                    sh "echo setURL"
                    sh "git push -u origin master"
                 }
            }
            post {
                    failure {
                      echo 'K8S Manifest Update failure !'
                    }
                    success {
                      echo 'K8S Manifest Update success !'
                    }
            }
        }
    }
}
