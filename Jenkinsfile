pipeline {
    agent any
    parameters {
        string(name: 'CF_USER', defaultValue: 'bluemix.workshop.user2@gmail.com')
        string(name: 'CF_PWD', defaultValue: 'FWFbN9@S')
        string(name: 'CF_ORG', defaultValue: 'bluemix.workshop.user2@gmail.com')
        string(name: 'CF_SPACE', defaultValue: 'dev')
        string(name: 'CF_APP_NAME', defaultValue: 'FWFbN9@S')
    }
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
                    cf login -u $CF_USER -p $CF_PWD -o $CF_ORG -s $CF_SPACE
                    echo "Deploying...."
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
