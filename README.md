# BC_Def_Auto2
Desafio de Automação - 02

# Instalar o postman:
https://www.postman.com/downloads/

# Instalar o CLI do postman:

https://learning.postman.com/docs/postman-cli/postman-cli-installation/

# Executar o runner (Windows) CMD:

postman collection run "C:/projects/BC_Def_Auto2/postman/collections/Col_BC_Def_Auto2" -e "C:/projects/BC_Def_Auto2/postman/environments/Dev.environment.yaml"

# Configurar a pipeline do Jenkins no Linux:
pipeline {
  agent any

  tools {nodejs "{your_nodejs_configured_tool_name}"}

  stages {
    stage('Install Postman CLI') {
      steps {
        sh 'curl -o- "https://dl-cli.pstmn.io/install/linux64.sh" | sh'
      }
    }

    stage('Postman CLI Login') {
      steps {
        sh 'postman login --with-api-key $POSTMAN_API_KEY'
        }
    }

    stage('Running collection') {
      steps {
        sh 'postman collection run "2659129-8c920553-7b71-460c-bb12-2a038ba09540"-e "f984dee6-15dc-442c-9bdb-5b6f4ef1417c"'
      }
    }
  }
}
