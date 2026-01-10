pipeline {
    agent {
        node {
            label 'linux && java17'
        }
    }
    
    stages {
        stage('Build') {
            steps {

                script {
                    for (int i = 0; i < 10; i++) {
                        echo ("Script ${i}")
                    }
                }
                echo ("Start Build")
                sh ("./mvnw clean compile test-compile")
                echo ("Start Build")
            }
        }

        stage ('Test') {
            steps {
                echo ("Start Test")
                sh ("./mvnw test")
                echo ("Start Test")
            }
        }

        stage ('Deploy') {
            steps {
                echo ('Hello Deploy 1')
                sleep(5)
                echo ('Hello Deploy 2')
                echo ('Hello Deploy 3')
            }
        }
    }

    post {
        always {
            echo " I will always say Hello again!"
        }
        success {
            echo "Yay, success"
        }
        failure {
            echo "oh no, failure"
        }
        cleanup {
            echo "Don't care success or error"
        }
    }
}