pipeline {
    agent any

    tools {
        maven 'jenkinsmaven'
        // jenkinsmaven 'Jenkinsmaven'
        // jdk 'Java11'
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
    }
}
