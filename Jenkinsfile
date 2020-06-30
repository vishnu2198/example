node{
   stage('test'){
     git 'https://github.com/AnithaRamachandranR/jenkins'
     }
   stage('Compile-Package'){
      // Get maven home path
    def mvn_home = 'maven'
    withEnv( ["PATH+MAVEN=${tool mvn_home}/bin"] ) {
     sh "mvn clean install"
    }
   }
   stage('Deploy to Tomcat'){
      sshagent(['tom']) {
      sh 'scp -o StrictHostKeyChecking=no target/*.war  ec2-user@52.90.68.233:/home/ec2-user/tomcat7/webapps/'
      }
  }
   stage('Deploy to airflow'){
    sshagent(['tom']) {
    sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/anithapip/*.py  ec2-user@52.90.68.233:/home/ec2-user/airflow/dags/'

     }
    sh 'pwd'
    dir('ec2-user@52.90.68.233:/home/ec2-user/airflow'){
    sh 'pwd'
    }
     sh 'airflow webserver -p 8080 & airflow scheduler && fg '
    }
   
}  
