pipeline {
  agent {
    docker {
      image "bryandollery/terraform-packer-aws-alpine"
      args "-u root --entrypoint='' --rm"
    }
  }
  environment {
    CREDS = credentials('bashayr')
    AWS_ACCESS_KEY_ID = "${CREDS_USR}"
    AWS_SECRET_ACCESS_KEY = "${CREDS_PSW}"
    OWNER = "bashayr"
    PROJECT_NAME = 'web-server'
    AWS_PROFILE="kh-labs"
    TF_NAMESPACE="bashayr"
  }
  stages {
      stage("init") {
          steps {
              sh 'make init'
              echo 'finsh init'
          }
      }
      stage("workspace") {
          steps {
              sh """
terraform workspace select jenkins-lab2
if [[ \$? -ne 0 ]]; then
  terraform workspace new jenkins-lab2
fi
"""
              echo 'finsh workspace'
          }
      }
      stage("plan") {
          steps {
              sh 'make plan'
          }
      }
      stage("apply") {
          steps {
              sh 'make apply'
          }
      }
  }
}
