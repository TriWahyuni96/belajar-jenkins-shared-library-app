@Library("belajar-jenkins-shared-library@master") _ 

import uni.jenkins.Output;
pipeline {
    agent any 
    stages {
        stage("Library Resource") {
            steps {
                script {
                    def config = libraryResource("config/build.json")
                    echo(config)
                }
            }
        }
        stage("Hello person") {
            steps {
                script {
                    hello.person ([
                        firstName: "Tri Wahyuni",
                        lastName: "Uni"
                    ])
                }
            }
        }
        stage("Maven Build") {
            steps {
                script {
                    maven(["clean", "compile", "test"])
                }
            }
        }
        stage("Global Variable") {
            steps {
                script {
                    echo(author())
                    echo(author.name())
                }
            }
        }
        stage("Hello Groovy") {
            steps {
                script {
                    Output.hello(this, "Groovy")
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