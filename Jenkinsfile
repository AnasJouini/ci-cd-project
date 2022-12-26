pipeline {
    agent any
    stages {
        stage('Cloning project') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'master', credentialsId: '1be0c2a9-8f2f-44b5-aafe-dae4362988b1', url: 'https://github.com/AnasJouini/ci-cd-project.git'
                echo "-------------------Clone Stage Done ------------------------------- "
            }
        }
        stage("MAVEN CLEAN") {
            steps {
                script {
                    sh "mvn -X -Dmaven.test.failure.ignore=true clean"
                }
            }
        }
        stage("MAVEN COMPILE") {
            steps {
                script {
                    sh "mvn -X -Dmaven.test.failure.ignore=true compile"
                }
            }
        }
        stage("MAVEN TEST") {
            steps {
                script {
                    sh "mvn -Dmaven.test.failure.ignore=true test"
                }
            }
        }
        stage("MAVEN BUILD") {
            steps {
                script {
                    sh "mvn -Dmaven.test.failure.ignore=true clean package"
                }
            }
        }
        stage('MAVEN BUILD & DEPLOY TO NEXUS REPO') {
            steps {
                echo 'Hello World'
                nexusArtifactUploader artifacts: [[artifactId: 'tpAchatProject', classifier: '', file: 'target/tpAchatProject-1.0.jar', type: 'jar']], credentialsId: 'a100b86b-708e-4c51-bddd-db3e6658cb2d', groupId: 'com.esprit.examen', nexusUrl: '192.168.125.110:8081/repository/maven-releases/', nexusVersion: 'nexus3', protocol: 'http', repository: 'nexusdeploymentrepo', version: '1.0'
            }
        }
        
    }    

}