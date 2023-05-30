pipeline {
    agent any

    tools {
        maven 'jenkinsmaven'
        //jenkinsmaven 'Jenkinsmaven'
        //jdk "Java11"
    }
    
    stages {
        stage('Build') {
            steps {
                // Obtén el código desde un repositorio de GitHub
                git branch: 'main', url: 'https://github.com/christianeduardoarosreuss/repomaven.git'
                
                // Ejecuta Maven en un agente Unix (Linux)
                sh "mvn clean package"
                
                // Archivar los artefactos generados
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
        
        stage('Test') {
            steps {
                // Ejecutar pruebas de Maven
                sh "mvn test"
            }
        }

             stage('Sonar Scanner') {
        steps {
            script {
                def sonarqubeScannerHome = tool name: 'sonar', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                withCredentials([string(credentialsId: 'sonar', variable: 'sonarLogin')]) {
                    sh "${sonarqubeScannerHome}/bin/sonar-scanner -e -Dsonar.host.url=http://SonarQube:9000 -Dsonar.login=${sonarLogin} -Dsonar.projectName=mv-maven -Dsonar.projectVersion=${env.BUILD_NUMBER} -Dsonar.projectKey=GS -Dsonar.sources=src/test/java/com/kibernumacademy/miapp -Dsonar.tests=src/test/java/com/kibernumacademy/miapp -Dsonar.language=java -Dsonar.java.binaries=."
                }
            }
        }
    }
}

