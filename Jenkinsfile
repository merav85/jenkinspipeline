pipeline {
    agent any
    
    /* parameters { 
         string(name: 'tomcat_stg', defaultValue: '54.194.123.193', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '34.241.180.58', description: 'Production Server')
    }  */

    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        echo "building staging"
                        //sh "scp -i /home/jenkins/tomcat.pem **/target/*.war ec2-user@${params.tomcat_stg}:/var/lib/tomcat7/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        echo "building production"
                        //sh "scp -i /home/jenkins/tomcat.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}