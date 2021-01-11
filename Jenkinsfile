pipeline {
    agent any
    parameters {
        string(name: 'STATEMENT', defaultValue: 'hello; ls /', description: 'What should I say?')
    }
    environment {
        // Using returnStdout
        CC = """${sh(
                returnStdout: true,
                script: 'echo "clang"'
            )}"""
        
    }

    stages {
        stage('Build') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                echo 'Building..'
                withCredentials([sshUserPrivateKey(credentialsId: 'GitHub', keyFileVariable: 'GH_KEY', passphraseVariable: 'PASS', usernameVariable: 'USR_NAME')]) {
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
                    //согласно доке, должна быть разница в выводе секретов между """ и '''
                    // """ должны быть менее секьюрны
                    // но разницы я не вижу.
                    //в обоих вариантах, cat $GH_KEY выведет в лог содержание private key
                }
                //вот тут видна разница
                sh("echo double-quotes")
                sh("echo ${STATEMENT}")
                sh('echo single-quotes')
                sh('echo ${STATEMENT}')
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