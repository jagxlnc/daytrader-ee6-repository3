pipeline {
    agent any
    stages {
        stage('Continuous Integration') {
            steps {
                sh '''
                   cd dt-ejb
                   mvn clean install
                   cd ../Rest
                   mvn clean install
                   cd ../web
                   mvn clean install
                   cd ../daytrader-ee6
                   mvn clean verify
                   cd ..
                   '''
             }
        }
        stage('Continuos Delivery') {
            steps {
                sh '''
                    pwd
                    cd daytrader-ee6/target
                    pwd
                    ls -la
                    echo "CF Login..."
                    cf api https://api.ng.bluemix.net
                    cf login -u bluemix.workshop.user2@gmail.com -p FWFbN9@S -o bluemix.workshop.user2@gmail.com -s dev
                    echo "Deploying...."
                    export CF_APP_NAME="dm-daytrader-ee6"
                    cf delete $CF_APP_NAME -f
                    cf push $CF_APP_NAME -n $CF_APP_NAME -p wlp/usr/servers/Daytrader3Sample
                '''
            }
        }
    }
}
