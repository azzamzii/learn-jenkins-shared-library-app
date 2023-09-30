@Library("learn-jenkins-shared-library@main") _

import programmerzamannow.jenkins.Output;

pipeline {
    agent any
    stages {
        stage("Hello person") {
            steps {
                script {
                    hello.person([
                        firstName: "Azzam",
                        middleName: "Zhafran",
                        lastName: "Imran"
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
        stage("Global variabel") {
            steps {
                script {
                    echo(author())
                    echo(author.name())
                    echo(author.channel())
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