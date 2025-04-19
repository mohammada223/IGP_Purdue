pipeline
{
	agent any
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
			    sh 'cp /var/lib/jenkins/workspace/$JOB_NAME/target/ABCtechnologies-1.0.war /var/lib/jenkins/workspace/$JOB_NAME/ABCtechnologies-1.0.war'
			    sh 'docker build -t arshadmckv/abc_tech:$BUILD_NUMBER .'
	
			}
		}

		stage('Push Docker Image')
		{ 
			steps
			{   
			    withDockerRegistry([ credentialsId: "dockerhub_id", url: "docker.io" ])
			    {   
			       sh 'docker push arshadmckv/abc_tech:$BUILD_NUMBER'
				   
			    }
			}
		}

		stage('Deploy as container')
		{
			steps
			{
				sh 'docker run -itd -P arshadmckv/abc_tech:$BUILD_NUMBER'
			}
		}

		
   }
}
