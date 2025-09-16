pipeline {
      agent {
	       label {
		           label 'built-in'
				   customWorkspace '/mnt/ws/'
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
			  cp target/SpringBootExecutableJarFileDemo-0.0.1-SNAPSHOT.jar  .
			  docker build -t rahulsgodase/myapp:${BUILD_NUMBER} .
			  '''
			  }
			 }
		  stage('s-3') {
		   steps {
                
           withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USR', passwordVariable: 'DOCKER_PSW')]) {
                    sh '''
                        echo $DOCKER_PSW | docker login -u $DOCKER_USR --password-stdin
                        docker push rahulsgodase/myapp:${BUILD_NUMBER}
                    '''
                }
                 }
               }
			  
			 }
         }
	
