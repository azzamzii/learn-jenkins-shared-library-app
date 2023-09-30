@Library("learn-jenkins-shared-library@main") _

import programmerzamannow.jenkins.Output;

pipeline {
    agent any
    stages {
        stage("Maven Build") {
            steps {
                script {
                    maven("clean compile")
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