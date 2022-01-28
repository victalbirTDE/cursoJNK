// Sintaxis declarativa: MAS SENCILLA y LA MAS USADA. Menos potente que la de scripting... 
//          pero mucho MAS que los proyectos de estilo libre
// Sintaxis de scripting: MAS COMPLEJA Y MAS POTENTE: Puedo hacer lo que quiera con Jenkins

pipeline {
    
    agent any
    
    stages {
        stage("Compilación") {
           steps{
              sh "mvn compile"
           }
        }
        stage("Pruebas") {
            stages {
                stage("Pruebas Dinámicas") {
                    stages {
                        stage("Compilación pruebas") {
                            steps {
                                sh "mvn test-compile"// Compilar pruebas -> Las pruebas no pueden ejecutarse
                            }
                        }
                        stage("Ejecución pruebas") {
                            steps {
                                sh "mvn test"// Ejecutar pruebas -> Genera informe... tanto si se ejecutan bien como si se ejecutan mal
                            }
                            post{
                                always {
                                 junit testResults: 'target/surefire-reports/*.xml' // Guardar el informe de pruebas <- 
                                }    
                            }
                        }
                    }
                }
                stage("SonarQube") {
                   steps{
                     sh """
                        mvn sonar:sonar -Dsonar.projectKey=miproyecto
                        -Dsonar.host.url=http://172.31.5.147:8081
                        -Dsonar.login=1f869cc7930343f1549e491b6d4710a8bc2643bc
                        """ 
                   }
                }
            }
        }
        stage("Empaquetado") {
            steps {
               sh "mvn package" // Empaquetar
            }
            post{
                success {
                  archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false // Guardar el artefacto (resultante del empaquetado)
                }
            }
        }
    }
    post {
        always {
            cleanWs() // Borrar el espacio de trabajo
        }
    }
}