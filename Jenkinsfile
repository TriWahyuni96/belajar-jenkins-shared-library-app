pipeline {
    agent none

    environment {
        AUTHOR = "Tri Wahyuni"
        EMAIL = "105841118423@student.unismuh.ac.id"
    }

    // triggers{
    //     cron("*/5 * * * *")
    // }

    parameters {
        string(name : "NAME", defaultValue : "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices:['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    options {
        disableConcurrentBuilds()
        timeout(time : 10, unit: 'MINUTES')
    }

    stages {

        stage("Preparation") {
          agent {
                node {
                    label 'linux && java17'
                }
            }  
        }
        stages {
            stage("Prepare Java") {
                steps {
                    echo("Prepare Java")
                }
            }
            stage("Prepare Maven") {
                steps {
                    echo("Prepare Maven")
                }
            }

        }

        stage('Parameter') {
            agent {
                node {
                    label 'linux && java17'
                }
            }
            steps {
                echo "Hello ${params.NAME}"
                echo "You description is ${params.DESCRIPTION}"
                echo "You social media is ${params.SOCIAL_MEDIA}"
                echo "Need to deploy : ${params.DEPLOY} to deploy!"
                echo "Your secret is ${params.SECRET}"
            }
        }
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
                sh('echo "App Password : $APP_PSW" > "rahasia.txt"')
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
            input {
                message "Can we deploy?"
                ok "Yes, of course"
                submitter "pzn, uni"
                parameters {
                    choice(name: "TARGET_ENV", choices: ['DEV', 'QA', 'PROD'], description: "Which Enviroment?")
                }
            }
            agent {
                node {
                    label 'linux && java17'
                }
            }
            steps {
              echo("Deploy to ${TARGET_ENV}")
            }
        }
        stage("Release"){
            when {
                expression {
                    return params.DEPLOY
                }
            }
           agent {
                node {
                    label 'linux && java17'
                }
            }
            steps {
                echo("Release it")
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