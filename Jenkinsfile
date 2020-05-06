pipeline {
    agent any
    tools {
        maven 'M3'
        jdk 'jdk8.221'
    }
    stages {
	
        stage ('Build') {
            steps {
                sh ("mvn -f P-Geo/pom.xml clean verify")
            }
            
        }
        stage('Ejecutar Pruebas'){
                steps{
                    script{
                        try{
 						sh ("mvn -f P-Geo/pom.xml verify package -P Rimac")
        				sh ("mvn -f P-Geo/pom.xml test -Dcucumber.options=\"src/test/resources/features/ --tags \'${ESCENARIO}\' --glue rimac\"")
        				sh ("mvn -f P-Geo/pom.xml serenity:aggregate")
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