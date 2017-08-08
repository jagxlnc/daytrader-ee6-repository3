pipeline {
    agent any
    stages {
        stage('Continuous Integration') {
            steps {
                sh '''
                   #cd dt-ejb
                   #mvn clean install
                   #cd ../Rest
                   #mvn clean install
                   #cd ../web
                   #mvn clean install
                   #cd ../daytrader-ee6
                   #mvn clean verify
                   #cd ..
                   '''
             }
        }
        stage('Continuous Delivery') {
            steps {
                sh '''
                    #!/bin/bash
                    cd daytrader-ee6/target
                    echo "CF Login..."
                    cf api https://api.ng.bluemix.net
                    cf login -u bluemix.workshop.user2@gmail.com -p FWFbN9@S -o bluemix.workshop.user2@gmail.com -s dev
                    echo "Deploying...."
                    export CF_APP_NAME="dm-daytrader-ee6"
                    if cf app $CF_APP_NAME; then
                    echo "Application already exists, pushing new version..."
                    cf push $CF_APP_NAME -n $CF_APP_NAME -p wlp/usr/servers/Daytrader3Sample
                    else
                    echo "New Application, push and restage required..."
                    cf push $CF_APP_NAME -n $CF_APP_NAME -p wlp/usr/servers/Daytrader3Sample
                    cf restage $CF_APP_NAME
                    fi
                '''
            }
        }
    }
}
