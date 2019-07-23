import groovy.json.JsonSlurper

// Parses the XML Publish profile and returns the username and password.
def getFtpPublishProfile(def publishProfilesJson) {
  def pubProfiles = new JsonSlurper().parseText(publishProfilesJson)
  for (p in pubProfiles)
    if (p['publishMethod'] == 'FTP')
      return [url: p.publishUrl, username: p.userName, password: p.userPWD]
}

node {
  stage('init') {
    // Check out the GitHub repo
    checkout scm
  }
  
  stage('build') {
    // Log in to Azure using the service principal
    withCredentials([azureServicePrincipal('jenkinsServicePrincipal')]) {
      sh '''
        az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID
        az account set -s $AZURE_SUBSCRIPTION_ID
      '''
    }
  
    // Build the JAR and zip it
    sh '''
        mvn clean package -Pproduction
        cd target
        zip application.zip app.jar
      '''
  }
  
  stage('deploy') {
    // Replace these values with your Resource Group and App Service name
    def resourceGroup = 'freebergJenkinsDemo' 
    def webAppName = 'freebergjava'

    // Get the publish profile username and password
    def pubProfilesJson = sh script: "az webapp deployment list-publishing-profiles -g $resourceGroup -n $webAppName", returnStdout: true
    def ftpProfile = getFtpPublishProfile pubProfilesJson

    // Deploy using the /wardeploy API on the Kudu site. We authenticate using the FTP username and password. (Username is just $<site-name>.)
    sh 'curl -X POST -u \\$freebergjava'+":${ftpProfile.password} --data-binary @target/application.zip https://${webAppName}.scm.azurewebsites.net/api/zipdeploy"
    
    // Log out
    sh 'az logout'
  }
}