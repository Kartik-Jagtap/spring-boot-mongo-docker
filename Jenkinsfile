node{
     
    stage('SCM Checkout'){
        git credentialsId: 'GIT_CREDENTIALS', url:  'https://github.com/MithunTechnologiesDevOps/spring-boot-mongo-docker.git',branch: 'master'
    }
    
    stage(" Maven Clean Package"){
      def mavenHome =  tool name: "Maven-3.6.1", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
      
    } 
    
    
    stage('Build Docker Image'){
        sh 'docker build -t kartikrj/spring-boot-mongo .'
    }
    
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'DOCKER_HUB_CREDENTIALS', variable: 'DOCKER_HUB_CREDENTIALS')]) {
          sh "docker login -u kartikrj -p ${DOCKER_HUB_CREDENTIALS}"
        }
        sh 'docker push kartikrj/spring-boot-mongo'
     }
	/**
     
     stage("Deploy To Kuberates Cluster"){
       kubernetesDeploy(
         configs: 'springBootMongo.yml', 
         kubeconfigId: 'KUBERNATES_CONFIG',
         enableConfigSubstitution: true
        )
     }
	 
	  /**
      stage("Deploy To Kuberates Cluster"){
        sh 'kubectl apply -f pringBootMongo.yml'
      } **/
     
}

