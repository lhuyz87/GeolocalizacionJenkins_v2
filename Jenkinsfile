pipeline {
    agent any
    tools {
        maven 'M3'
        jdk 'jdk8.221'
    }
    stages {
	
        stage ('Build') {
            steps {
                sh ("mvn clean verify")
            }
            
        }
        stage('Ejecutar Pruebas'){
                steps{
                    script{
                        try{
 						sh ("mvn verify package -P Rimac")
        				sh ("mvn test -Dcucumber.options=\"src/test/resources/features/ --tags \'${ESCENARIO}\' --glue rimac\"")
        				sh ("mvn serenity:aggregate")
        				echo 'Ejecucion de pruebas sin errores...'
                         }
                        catch(ex)
                        {    
                            echo 'Finalizo ejecucion con fallos'
                            error('Failed')
                        }
                    }
                }
                
            }
            
   /*            stage('Reporte'){
            steps{
                script{ 
                    try{
                    	sh ("echo ${defTimestamp}")
                    	publishHTML([allowMissing: true, alwaysLinkToLastBuild: true, keepAll: true, reportDir: "/var/lib/jenkins/workspace/P-RegresionVidaLeyGrupo/target/site/serenity", reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: ''])
                         echo 'Reporte realizado con exito'
                    }
                    catch(ex)
                    {    
                        echo 'Reporte realizado con Fallos'
                        error('Failed')
                    }
                }
            }
        }*/
    }
}