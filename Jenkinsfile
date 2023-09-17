pipeline {
  agent {label 'two-tier'}
     stages {
	   stage ('code'){
	      steps {
		    echo "clone code"
			git url:"https://github.com/dipakbhagade/two-tier-flask-app.git", branch:'master'
		  }
	   }
	   stage ('build and test'){
	      steps {
		    echo "build and testing"
			sh 'docker build . -t dipak1994/two-tier-app:latest'
		  }
	   }
	   stage ('image push to dockerHub'){
	      steps {
		    echo "push image to dockerHub"
			withCredentials([usernamePassword(credentialsId:'two-tier-dockerHub',passwordVariable:'dockerHubPassword',usernameVariable:'dockerHubUser')]){
			sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
			sh 'docker push dipak1994/two-tier-app:latest'
			}
		  }
	   }
	   stage ('Deploy'){
	      steps {
		    echo "deployment"
			sh "docker-compose down && docker-compose up -d"
		  }
	   }
	 }
}
