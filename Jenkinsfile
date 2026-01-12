@Library("belajar-jenkins-shared-library@master") _ 

import uni.jenkins.Output;
pipeline {
    agent any 
    stages {
        stage("Hello World") {
            steps {
                script {
                    Output.hello("Groovy")
                }
            }
        }
        stage("Hello World") {
            steps {
                script {
                    hello.world()
                }
            }
        }
    }
}