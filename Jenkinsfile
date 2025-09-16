pipeline {
      agent {
	       label {
		           label 'built-in'
				   customWorkspace '/root/'
				   }
			}
	 stages {
	     stage('s-1') {
		    steps {
			    sh " mvn clean install "
				}
			}
	     stage('s-2') {
		   steps {
		      sh '''
			  cd /root/
			  docker build -t myusername/myapp:${BUILD_NUMBER} .
			  '''
			  }
			 }
		  stage('s-3') {
		   steps {
                
            
            sh ''' 
			       cd /root/
			       echo $DOCKER_PSW | docker login -u $DOCKER_USR --password-stdin
                   
                   docker push myusername/myapp:${BUILD_NUMBER}
				  
				  '''
                 }
               }
			  
			 }
         }
	
