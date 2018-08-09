// jenkinsfiles
node {
   def mvnHome
   stage('Preparation') {
      git 'git@bitbucket.org:khzied/project1-maven.git'
      mvnHome = tool 'maven'
   }
   stage('Build') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      archiveArtifacts 'target/*.war'
   }
   stage('Publish') {    
    nexusPublisher nexusInstanceId: 'Local-Nexus', nexusRepositoryId: 'project-release', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: '/var/jenkins_home/workspace/Pipeline-Build-DeploytoNexus/target/example.war']], mavenCoordinate: [artifactId: 'site1', groupId: 'com.example.maven', packaging: 'war', version: 'myapp-v1-"${BUILD_TIMESTAMP}"']]]          
   }
}