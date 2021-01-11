pipeline {
    agent any

    environment {
        // Using returnStdout
        CC = """${sh(
                returnStdout: true,
                script: 'echo "clang"'
            )}"""
        withCredentials([sshUserPrivateKey(credentialsId: 'GitHub', keyFileVariable: 'GH_KEY', passphraseVariable: 'PASS', usernameVariable: 'USR_NAME')]) {
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
                    echo $GH_KEY
                """
                echo 'Second output'
                sh '''
                    set +x
                    echo $GH_KEY
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