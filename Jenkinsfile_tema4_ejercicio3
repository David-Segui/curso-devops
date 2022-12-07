pipeline {
    agent any
    stages {
        stage('Get Code') {
            steps {
                // Hace un git Clone del codigo - Nota: La rama pripal por defecto es master, sino especificar.
                git branch: 'devel', url: 'https://github.com/David-Segui/curso-devops.git'
                
                //Llamada a git especificando la rama por defecto
                //checkout([$class: 'GitSCM',
                //    branches: [[name: 'devel']],
                //    userRemoteConfigs: [[url: 'https://github.com/David-Segui/curso-devops.git']]])
                
                //bat "git.exe clone https://github.com/David-Segui/curso-devops.git"
                
            }
        }
        stage('Build') {
            steps {
                bat "echo %WORKSPACE%"
                bat "dir"
            }
        }
        stage('test') {
            parallel
            {
                // Test Unitarios
                stage('Unit') {
                    steps {
                        catchError(buildResult: "UNSTABLE", stageResult: "FAILURE") {
                  
                        bat '''
                            cd .\\Tema-04\\Ejercicio1
                        
                            REM ">>>> Asignamos las variables de entorno para Python"
                            set PATH=%PATH%;C:\\Users\\david\\AppData\\Local\\Programs\\Python\\Python311\\Scripts;C:\\Users\\david\\AppData\\Local\\Programs\\Python\\Python311
                            set PYTHONPATH=.
                        
                            REM ">>>> Ejecutamos las pruebas unitarias"
                            pytest --junitxml=result-unix.xml test\\unit 
                        '''
                        //NOTA:La salida de pytest lo guardamos en un fuchero xml
                        }
                    }
                }
                // Test Rest
                stage('Rest') {
                    steps {
                        catchError(buildResult: "UNSTABLE", stageResult: "FAILURE") {
                        
                            bat '''
                                cd .\\Tema-04\\Ejercicio1
                        
                                REM ">>>> Asignamos las variables de entorno para Python"
                                set PATH=%PATH%;C:\\Users\\david\\AppData\\Local\\Programs\\Python\\Python311\\Scripts;C:\\Users\\david\\AppData\\Local\\Programs\\Python\\Python311
                                set PYTHONPATH=.
                        
                                REM ">>>> Asignamos las variables de entorno para Flask"
                                SET FLASK_APP=app\\api.py
                        
                                REM ">>>> Iniciamos el servicio  Flask"
                                start flask run
                        
                                REM ">>>> Iniciamos el Wiremock
                                start java -jar C:\\Users\\david\\Downloads\\wiremock-jre8-standalone-2.35.0.jar  --port 9090 --root-dir test\\wiremock
                        
                                REM ">>>> Ejecutamos las pruebas unitarias de rest"
                                pytest --junitxml=rest-unix.xml test\\rest
                            '''
                        //NOTA:La salida de pytest lo guardamos en un fuchero xml
                        }
                    }
                }
            }
        }
        stage('Finish') {
            steps {
                    bat 'echo "---FIN---"'
            }
        }
    }
    post {
        always {
            echo 'The pipeline completed'
            junit allowEmptyResults: true, testResults:'**/test_reports/*.xml'
        }
        success {                   
            echo "All OK!!"
        }
        failure {
            echo 'Build stage failed'
            error('Stopping early…')
        }
      }
}
