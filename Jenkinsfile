pipeline {
    agent none

    environment {
        AUTHOR = "Azzam Zhafran Imran"
    }

    // triggers {
    //     cron("*/5 * * * *")
    // }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    options {
        disableConcurrentBuilds()
        timeout(time:10, unit: 'MINUTES')
    }

    stages {

        stage("Parameter") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo "Hello ${params.NAME}!"
                echo "Your description is ${params.DESCRIPTION}"
                echo "Your social media ${params.SOCIAL_MEDIA}"
                echo "Need to deploy : ${params.DEPLOY} to deploy!"
                echo "Your secret is ${params.SECRET}"
            }
        }

        stage("Prepare") {
            environment {
                APP = credentials ("azzam-secret")
            }
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps{
                echo ("Author ${AUTHOR}")
                echo ("App User : ${APP_USR}")
                sh ("echo 'App Password : ${APP_USR}' > 'secret single quote.txt'")
                sh ('echo "App Password : $APP_PSW" > "secret double quote.txt"')
                echo ("Start Job    : ${env.JOB_NAME}")
                echo ("Start Build  : ${env.BUILD_NUMBER}")
                echo ("Branch Name  : ${env.BRANCH_NAME}")
            }
        }
        stage("Build") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps{
                script {
                    def data = [
                        "firstName" : "Azzam",
                        "lastName" : "Imran"
                    ]
                    writeJSON(file: "data.json", json:data)
                }
                echo("Start Build")
                sh("./mvnw clean compile test-compile")
                echo ("Finish Build")
            }
        }
        stage("Test") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps{
                echo("Start Test")
                sh("./mvnw test")
                echo ("Finish Test")
            }
        }
        stage("Deploy") {

            input {
                message "Can we deploy?"
                ok "Yes, of course"
                submitter "azzamzhafran_i"
                parameters {
                    choice(name: "TARGET_ENV", choices: ['DEV', 'QA', 'PROD'], description: "Which Environment?")
                }
            }

            agent {
                node {
                    label "linux && java11"
                }
            }

            steps{
                echo "Deploy to ${TARGET_ENV}"
            }
        }                
    }
    
    post {
        always {
            echo "I always say Hello again!"
        }
        success {
            echo "Yay, success"
        }
        failure {
            echo "Oh no, failure"
        }
        cleanup {
            echo "Don't care success or error"
        }
    }
}