pipeline {
    agent any

    environment {
        // Using returnStdout
        CC = """${sh(
                returnStdout: true,
                script: 'echo "clang"'
            )}"""
        withCredentials([sshUserPrivateKey(credentialsId: 'GitHub', keyFileVariable: 'GH_KEY', passphraseVariable: '', usernameVariable: '')]) {
    // some block
        }
    }

    stages {
        stage('Build') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                echo 'Building..'
                echo 'First output'
                sh """
                    set +x
                    echo $GitHub
                """
                echo 'Second output'
                sh '''
                    set +x
                    echo $GitHub
                '''
            }
        }
        stage('Test') {
            environment { 
                DEBUG_FLAGS = '-g'
            }
            steps {
                echo 'Testing..'
                sh 'printenv'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}