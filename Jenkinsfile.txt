pipeline
{
	agent any
	stages
	{
		stage('Code Checkout')
		{
			steps
			{
				git 'https://github.com/jsachdev07/igp-mar22.git'
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
   }
}
