node {
   stage('Preparation') {
      git 'https://github.com/chrisc1122/fleetman-webapp'
   }
   stage('Build') {
      sh "mvn clean package"
   }
   stage('Results') {
      archive 'target/*.war'
   }
   stage('Deploy') {
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-credentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
         ansiblePlaybook credentialsId: 'ssh-credentials', installation: 'ansible-installation', playbook: 'deploy.yaml'
      }
   }
}
