pipeline{
    
   tools{
     jdk 'myjdk'
     maven 'mymaven'
     }
     
    agent {label 'Slave1'}
    
    stages{
        
        
        stage('checkout'){
            steps{
                git 'https://github.com/akn4039/DevOpsClassCodes.git'
            }
        }
            stage('compile'){
                steps{
                    sh 'mvn compile'
                }
                
            }
            stage ('code review'){
                steps{
                    sh 'mvn pmd:pmd'
                }
            }
            stage ('test'){
                steps{
                    sh 'mvn test'
                }
                post{
                    success{
                        junit 'target/surefire-reports/*.xml'
                        
                    }
                }
            }
            stage ('code coverage'){
                steps{
                    sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
                }
                post{
                    success{
                        cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
                    }
                }
            }
            stage('Package'){
                steps{
                    sh 'mvn package'
                    echo 'Welldone pipeline is completed'
                }
            }
        }
}
    
