pipeline {
    options {
        // set a timeout of 30 minutes for this pipeline
        timeout(time: 30, unit: 'MINUTES')
    }
    agent {
      node {
        label 'master'
      }
    }

    stages {

        stage('stage 1') {
            steps {
                script {
                    openshift.withCluster() {
                        openshift.withProject() {
                                echo "stage 1: using project: ${openshift.project()} in cluster ${openshift.cluster()}"
                        }
                    }
                }
            }
        }

        // TODO: ADD A STAGE THAT SAYS HELLO

        stage('stage 2') {
          steps {
            script {
              echo "Hello master"
            }
          }

        }
        // TODO: ADD AN APPROVAL STAGE

        stage('approval') {
          steps {
            timeout(time: 10, unit: 'MINUTES') { 
              input message: "Move to stage 3?" 
            }
          }
        }
        stage('stage 3') {
            steps {
                sh 'echo hello from stage 3!. This is the last stage...'
            }
        }

    }
}

