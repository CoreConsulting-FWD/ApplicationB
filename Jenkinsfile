pipeline {
  agent {
      label 'built-in'
  }
  stages {
    stage('Checkout Repositories') {
      steps {
        echo 'Git pull request on latest commit'
      }
    }

    stage('Approve Staging Deployment') {
      steps {
        echo 'Notifying PIC'
        input 'Confirm Staging Deployment'
      }
    }

    stage('Staging Deployment') {
      parallel {
        stage('Staging Deployment') {
          steps {
            sh 'echo "Deploy Application A"'
          }
        }

        stage('Cleaning Staging') {
          steps {
            sh '''echo "Cleaning Staging Environment"

                sleep 2'''
          }
        }

        stage('Deploying Application') {
          steps {
            sh '''echo "Deploying Application to Staging Environment"

                sleep 2'''
          }
        }

        stage('Status Report') {
          steps {
            sh 'echo "Deployment Status"'
          }
        }

      }
    }

    stage('Approve Core Function Test') {
      steps {
        echo 'Notifying PIC'
        input 'Confirm Core Function Test?'
      }
    }

    stage('Core Function Test') {
      parallel {
        stage('Core Function 1') {
          steps {
            echo "Commencing Core Function Test 2 on Application A"
            echo "Init Selenium"
            sh "sleep 3"
            echo "Function Test 1 PASSED!"
          }
        }

        stage('Core Function 2') {
          agent {
            label 'kitkat'
          }
          steps {
            echo "Commencing Core Function Test 2 on Application A"
            bat '''cd C:\\Jenkins_Agent
                   java -jar 2ndTest.jar 
             '''
            echo "Function Test 2 PASSED!"
          }
        }

        stage('Core Function 3') {
          agent {
            label 'kitkat'
          }
          steps {
            echo "Commencing Core Function Test 3 on Application A"
            bat '''cd C:\\Jenkins_Agent
                   java -jar firstTest.jar 
             '''
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
               sh "exit 1"
            }

          }
        }

        stage('Core Function N') {
          steps {
            echo "Commencing Core Function Test N on Application A"
            echo "Init Selenium"
            sh "sleep 3"
            echo "Function Test 3 PASSED!"
          }
        }
      }
    }

    stage('Approve Production Deployment') {
      steps {
        echo 'Notifying PIC'
        input 'Confirm Production Deployment'
      }
    }

    stage('Production Deployment') {
      parallel {
        stage('Production Deployment') {
          steps {
           echo "Deploying to Production Environment"

          }
        }

        stage('Cleaning Production') {
          steps {
            echo "Cleaning Production Environment"
            sh '''sleep 2'''
          }
        }

        stage('Deploying Application') {
          steps {
            echo "Deploying Application"
            sh '''sleep 5'''
          }
        }

        stage('Status Report') {
          steps {
            echo "Deployment Status"
          }
        }

      }
    }

  }
}
