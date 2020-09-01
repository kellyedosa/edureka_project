pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
    agent none
        stages{
             stage('Compile'){
                agent any
                steps{
                    sh 'mvn compile'
                }
                
            }
            stage('CodeReview'){
                agent any
                steps{
                    sh 'mvn pmd:pmd'
                }
                post{
                    always{
                        pmd pattern: 'target/pmd.xml'
                    }
                }
            }
            stage('UnitTest'){
                agent any
                steps{
                    git 'https://github.com/kellyedosa/edureka_project.git'
                    sh 'mvn test'
                }
                
            }
            stage('MetriCheck'){
                agent any
                steps{
                    sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
                }
                post{
                    always{
                        cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                    }
                }
            }
            stage('Package'){
                agent any
                steps{
                    sh 'mvn package'
                }
            }
            
        }
    
    }
