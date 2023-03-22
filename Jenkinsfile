pipeline {

  agent any
  environment {
    BRANCH_NAME = "${GIT_BRANCH.split("/")[1]}"
    DOCKER_TAG="${GIT_BRANCH.tokenize('/').pop()}-${GIT_COMMIT.substring(0,7)}"
    GIT_CREDENTIAL_ID='token-github1'
    
  }
  stages {
        // stage('check out') {
        //   steps{
        //     checkout scm
        //   }
        // }
        stage('Git Clone') {
            steps {
              // echo $(env.GIT_BRANCH)
              // echo env.GIT_URL
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                        git branch: "${BRANCH_NAME}", credentialsId: "${GIT_CREDENTIAL_ID}", url: "${env.GIT_URL}"
                }
            }
        }
        stage('Check Version Code') {
                    steps {
                        script {
                              def PACKAGE_VERSION = sh(script: "grep \"version\" package.json | cut -d '\"' -f4 | tr -d '[[:space:]]'", returnStdout: true)
                              sh "echo $PACKAGE_VERSION"
                              sh "pwd"

                            }
                        }
                    }
        }
  

  post {
    success {
      echo "SUCCESSFUL"
    }
    failure {
      echo "FAILED"
    }
  }
}