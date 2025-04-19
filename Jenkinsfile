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
			    sh 'cp /var/lib/jenkins/workspace/$JOB_NAME/target/abctechnologies.war /var/lib/jenkins/workspace/$JOB_NAME/abctechnologies.war'
				
                sh 'docker build -t mohammada223/IGP Pipeline Purdue:$BUILD_NUMBER .'

			}
		}

		stage('Push Docker Image')
		{ 
			steps
			{   
			    withDockerRegistry([ credentialsId: "dockerhub", url: "" ])
			    {   
			       sh 'docker push mohammada223/IGP Pipeline Purdue:$BUILD_NUMBER'
				   
			    }
			}
		}

		stage('Deploy as container')
		{
			steps
			{
				sh 'docker run -itd -P mohammada223/IGP Pipeline Purdue:$BUILD_NUMBER'
			}
		}

		
   }
}
