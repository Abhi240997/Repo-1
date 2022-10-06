
pipeline 
{
	
	agent any
	

	stages 
	{
		stage('Build Application') 
		{
		
			steps 
			{
				echo "Environment is"
				echo "dev"
				bat 'mvn clean install -DskipTests'
			
			}
		
		}
		
		stage('Test') 
		{
			environment {
        			ENV_NAME = "dev"
					SECURE_KEY = "Apisero_Dart"
    			}
			steps 
			{
				
			
				echo 'Application in Testing Phase… '
				echo "dev"
				bat "mvn test -Dmule.env=dev -Dmule.encryptionKey=Apisero_Dart -Dapp.coverage=60"
			
			}
		
		}
		
		stage('Deploy CloudHub') 
		{
		
			environment 
			{ 
				ANYPOINT_CREDENTIALS = credentials('anypointPlatforms')
		
			}
		
			steps 
			{
			
				echo 'Deploying mule project due to the latest code commit…'
				
				echo 'Deploying to the configured environment….'
				
				bat "mvn package deploy -DmuleDeploy -DskipTests -Dmule.env=dev -Dmule.encryptionKey=Apisero_Dart -Dapp.coverage=60 -Denv.name=DEV -Danypoint.uri=https://anypoint.mulesoft.com -Dmule.version=4.4.0 -Dcloudhub.user=${ANYPOINT_CREDENTIALS_USR} -Dcloudhub.password=${ANYPOINT_CREDENTIALS_PSW} -Dcloudhub.workerType=MICRO -Dcloudhub.workerCount=1 -Dcloudhub.region=us-east-2 -Danypoint.monitoring=false -Denv.suffix=-dev"
				
			}
		
		}
	
	}

}
