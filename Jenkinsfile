pipeline {
  agent any

  tools {
    nodejs 'nodejslocal' // Uses Node.js configured in Jenkins
  }

  environment {
    COLLECTION_ID = '11319530-de7a37d8-307f-49db-b656-f4ef0424a320'
    DATA_FILE = 'product_data.json'
    GLOBALS_FILE = 'workspace.postman_globals.json'
  }

  stages {
    stage('Postman CLI Login') {
      steps {
        withCredentials([string(credentialsId: 'postman-api-key', variable: 'POSTMAN_API_KEY')]) {
          bat 'postman login --with-api-key %POSTMAN_API_KEY%'
        }
      }
    }

    stage('Run Postman Collection') {
      steps {
        bat 'postman collection run %COLLECTION_ID% -d "%DATA_FILE%" -g "%GLOBALS_FILE%" -r html'
      }
    }
  }
}
