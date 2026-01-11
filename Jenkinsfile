pipeline {
    agent none

    environment {
        AUTHOR = "Tri Wahyuni"
        EMAIL = "105841118423@student.unismuh.ac.id"
    }

    stages {
        stage('Prepare') {
            environment {
                APP = credentials("uni_rahasia")
            }

            agent {
                node {
                    label 'linux && java17'
                }
            }
            steps {
                echo("Author ${AUTHOR}")
                echo("Email ${EMAIL}")
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NAME}")
                echo("Branch Name : ${env.BRANCH_NAME}")
                echo("APP User : ${APP_USR}")
                echo("APP Password : ${APP_PSW}")
            }
        }

        stage('Build') {
            agent {
                node {
                    label 'linux && java17'
                }
            }
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
            agent {
                node {
                    label 'linux && java17'
                }
            }
            steps {

                script {
                    def data = [
                        "firstName" : "Tri",
                        "LastName" : "Wahyuni"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
                echo ("Start Test")
                sh ("./mvnw test")
                echo ("Start Test")
            }
        }

        stage ('Deploy') {
            agent {
                node {
                    label 'linux && java17'
                }
            }
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