Pipeline {
    Agent {
        Node {
            Label 'SLAVE01'
        }
    }

    Tools {
        Maven 'maven3'
    }

    Options {
        BuildDiscarder LogRotator(
            DaysToKeepStr: '15',
            NumToKeepStr: '10'
        )
    }

    Environment {
        APP_NAME = "DCUBE_APP"
        APP_ENV = "DEV"
    }

    Stages {
        Stage('Cleanup Workspace') {
            Steps {
                CleanWs()
                Sh 'echo "Cleaned Up Workspace for ${APP_NAME}"'
            }
        }

        Stage('Code Checkout') {
            Steps {
                Checkout([
                    $class: 'GitSCM',
                    Branches: [[name: '*/master']],
                    UserRemoteConfigs: [[url: 'https://github.com/spring-projects/spring-petclinic.git']]
                ])
            }
        }

        Stage('Code Build') {
            Steps {
                Sh 'mvn install -Dmaven.test.skip=true'
            }
        }

        Stage('Printing All Global Variables') {
            Steps {
                Sh 'env'
            }
        }
    }
}
