
pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
    agent none
      stages{
           stage('Checkout'){
	    agent any
               steps{
		 echo 'cloning..'
                 git 'https://github.com/Bikash376919/code-test.git'
              }
          }
          stage('Compile'){
              agent any
              steps{
                  echo 'compiling..'
                  sh 'mvn compile'
	      }
          }
          stage('CodeReview'){
              agent any
              steps{
		  echo 'codeReview'
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
		   agent any
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
               agent any
              steps{
                  sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
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
