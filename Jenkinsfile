
pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
      stages{
           stage('Checkout'){
		   agent {label 'slave1'}
               steps{
		 echo 'cloning..'
                 git 'https://github.com/Bikash376919/code-test.git'
              }
          }
          stage('Compile'){
              agent {label 'slave1'}
              steps{
                  echo 'compiling..'
                  sh 'mvn compile'
	      }
          }
          stage('CodeReview'){
              agent {label 'slave1'}
              steps{
		  echo 'codeReview'
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
		   agent {label 'slave1'}
              steps{
	         
                  sh 'mvn test'
              }
               post {
               success {
                   junit 'target/surefire-reports/*.xml'
               }
           }	
          }
           stage('MetricCheck'){
               agent {label 'slave1'}
              steps{
                  sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
              }
               	
          }
          stage('Package'){
              agent {label 'slave1'}
              steps{
                  sh 'mvn package'
              }
          }
	     
          
      }
}
