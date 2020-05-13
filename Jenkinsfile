pipeline {

   agent any
   triggers { pollSCM('H/1 * * * *') }
   environment {
        OKTA_OAUTH2_ISSUER           = 'https://dev-957490.okta.com/oauth2/default'
        OKTA_OAUTH2_CLIENT_ID        = credentials('OKTA_OAUTH2_CLIENT_ID')
        OKTA_OAUTH2_CLIENT_SECRET    = credentials('OKTA_OAUTH2_CLIENT_SECRET')
   }

   stages {

      stage('Build') {

         steps {
            git 'https://github.com/tongancity/demo-app.git'
            sh "./mvnw -Dmaven.test.failure.ignore=true clean package"
         }


         post {

            success {

               junit '**/target/surefire-reports/TEST-*.xml'

               archiveArtifacts 'target/*.jar'

            }
         }

      }

   }

}