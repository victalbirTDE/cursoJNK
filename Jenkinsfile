// Sintaxis declarativa: MAS SENCILLA y LA MAS USADA. Menos potente que la de scripting... 
//          pero mucho MAS que los proyectos de estilo libre
// Sintaxis de scripting: MAS COMPLEJA Y MAS POTENTE: Puedo hacer lo que quiera con Jenkins

pipeline {
    
    agent any // Para definir DONDE QUIERO QUE SE EJECUTE ESTA TAREA
    //Parametros
    //Triggers
    stages {
       stage("Compilación") {
           steps { // Hacemos las llamadas a los plugins
               sh "mvn compile" // Llamada a compilacion Maven
           }
           post {
               always { // Post tareas que siempre deben de ejecutarse
                  sh "echo Acabó la compilación"
               }
               success { // Postareas que SOLO se ejecutan si los pasos (STEPS) han ido bien
                  sh "echo Y acabó bien"
               }
               failure { // Postareas que SOLO se ejecutan si los pasos (STEPS) han dado error
                  sh "echo Pero acabó mal"
               }
           }
       }
       stage("Compilación de pruebas") {
            steps { // Hacemos las llamadas a los plugins
               sh "mvn test-compile" // Llamada a compilacion de pruebas Maven
           }
           post {
               always { // Post tareas que siempre deben de ejecutarse
                  sh "echo Acabó la compilación de pruebas"
               }
               success { // Postareas que SOLO se ejecutan si los pasos (STEPS) han ido bien
                  sh "echo Y acabó bien"
               }
               failure { // Postareas que SOLO se ejecutan si los pasos (STEPS) han dado error
                  sh "echo Pero acabó mal"
               }
           }
           
       }
       stage("Pruebas") {
           steps { // Hacemos las llamadas a los plugins
               sh "mvn test" // Llamada a ejecución de pruebas Maven
           }
           post {
               always { // Post tareas que siempre deben de ejecutarse
                  sh "echo Acabó la ejecución de pruebas"
                  junit 'target/surefire-reports/*.xml'
               }
               success { // Postareas que SOLO se ejecutan si los pasos (STEPS) han ido bien
                  sh "echo Y acabó bien"
               }
               failure { // Postareas que SOLO se ejecutan si los pasos (STEPS) han dado error
                  sh "echo Pero acabó mal"
               }
           }
       }
       stage("Empaquetado") {
           steps { // Hacemos las llamadas a los plugins
               sh "mvn package" // Llamada a creación del paquete
           }
           post {
               always { // Post tareas que siempre deben de ejecutarse
                  sh "echo Acabó el empaquetado"
               }
               success { // Postareas que SOLO se ejecutan si los pasos (STEPS) han ido bien
                  sh "echo Y acabó bien"
                  archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
               }
               failure { // Postareas que SOLO se ejecutan si los pasos (STEPS) han dado error
                  sh "echo Pero acabó mal"
               }
           }
       }
    }

    post {
       always { // Post tareas que siempre deben de ejecutarse
          sh "echo Acabó la etapa 2"
       }
       success { // Postareas que SOLO se ejecutan si los pasos (STEPS) han ido bien
          sh "echo Y acabó bien"
       }
       failure { // Postareas que SOLO se ejecutan si los pasos (STEPS) han dado error
          sh "echo Pero acabó mal"
       }
    }
}