pipeline
{
	agent any
	environment {
        DOCKER_IMAGE = "arshadmckv/abc_tech"
        WORK_DIR = "/var/lib/jenkins/workspace/IGPWorkflow_1"
    }
	stages
	{
		stage('Code Checkout')
		{
			steps
			{
				git 'https://github.com/mohammada223/IGP_Purdue.git'
			}
		}
		
		stage('Code Compile')
		{
			steps
			{
				sh 'mvn compile'
			}
			
		}
		
		stage('Unit Test')
		{
			steps
			{
				sh 'mvn test'
			}
		}

		stage('Code packaging')
		{
			steps
			{
				sh 'mvn package'
			}
		}

stage('Build Docker Image')
		{
			steps
			{
			    sh 'cp ${WORK_DIR}/target/ABCtechnologies-1.0.war ${WORK_DIR}/abc_tech.war'
                	    sh 'docker build -t ${DOCKER_IMAGE}:latest .'
	
			}
		}

		stage('Push Docker Image')
		{ 
			steps
			{   
			    withDockerRegistry([ credentialsId: "dockerhub_id", url: "" ])
			    {   
			       sh 'docker push ${DOCKER_IMAGE}:latest'
				   
			    }
			}
		}

		stage('Deploy as container')
		{
			steps
			{
				sh 'docker run -itd -p 9090:9090 --name abcapp_1 ${DOCKER_IMAGE}:latest'
			}
		}

		stage('Deploy to kubernetes')
		{
			steps
			{
				sh 'kubectl apply -f deploy.yaml'
				sh 'kubectl apply -f service.yaml'
			}
		}
		
   }
}
