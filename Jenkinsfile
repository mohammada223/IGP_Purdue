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
   }
}
