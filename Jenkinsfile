

import groovy.json.JsonSlurperClassic

def jsonParse(def json) {

    new groovy.json.JsonSlurperClassic().parseText(json)

}

pipeline {

    agent any

    stages {

        stage("Paso 0: Download and checkout"){

            steps {

                checkout(

                    [$class: 'GitSCM',

                    //Acá reemplazar por el nonbre de branch

                    branches: [[name: "circleci" ]],

                    //Acá reemplazar por su propio repositorio

                    userRemoteConfigs: [[url: 'https://github.com/iordenes/ejemplo-maven']]])

            }

        }

        stage("Paso 1: Análisis SonarQub"){

            steps {

                withSonarQubeEnv('sonarqube') {

                    sh "echo 'Calling sonar Service in another docker container!'"

                    // Run Maven on a Unix agent to execute Sonar.

                    sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=job-github-sonar-1'

                }

            }

        }

    }

    post {

        always {

            sh "echo 'fase always executed post'"

        }

        success {

            sh "echo 'fase success'"

        }

        failure {

            sh "echo 'fase failure'"

        }

    }

}


