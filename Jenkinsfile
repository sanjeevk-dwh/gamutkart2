pipeline {
    agent any

        tools {
                maven 'Maven3.6'
        }

//      environment {
//              M2_INSTALL = "/home/gamut/Distros/apache-maven-3.6.0/bin/mvn"
//      }

    stages {
                stage('Clone-Repo') {
                        steps {
                                checkout scm
                        }
                }
                stage('Build') {
                steps {
                                sh 'mvn install -DskipTests'
                        }
            }
                stage('Unit Tests') {
                        steps {
                                sh 'mvn surefire:test'
                        }
                }
                stage('Deployment') {
                steps {
                                sh 'sshpass -p "sanjeev" scp target/gamutkart.war sanjeev@172.17.0.4:/home/sanjeev/distros/apache-tomcat-8.5.43/webapps'
                                sh 'sshpass -p "sanjeev" ssh sanjeev@172.17.0.4 "JAVA_HOME=/home/sanjeev/distros/jdk1.8.0_221" "/home/sanjeev/distros/apache-tomcat-8.5.43/bin/startup.sh"'
                }
                }
    }
}

