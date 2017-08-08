pipeline {
    agent any
    stages {
        stage('build') {
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
        stage('ICp-deploy') {
            steps {
                sh '''
                    kubectl config set-cluster cfc --server=https://172.21.20.136:8001 --insecure-skip-tls-verify=true
                    kubectl config set-context cfc --cluster=cfc
                    kubectl config set-credentials user --token=eyJhbGciOiJSUzI1NiIsImtpZCI6IjY5NjI2ZDJkNjM2NjYzMmQ3MzY1NzI3NjY5NjM2NTJkNmI2NTc5NjkiLCJ0eXAiOiJKV1QifQ.eyJhdWQiOiJjZmMtc2VydmljZSIsImV4cCI6MTUwMjE3MjU4NCwiaWF0IjoxNTAyMTI5Mzg0LCJpc3MiOiJodHRwczovL21hc3Rlci5jZmM6ODQ0My9hY3MvYXBpL3YxL2F1dGgiLCJwcm9qZWN0cyI6WyJkZWZhdWx0Il0sInN1YiI6ImFkbWluIn0.miiNXsFU-YhdvDDBIriJuc_kIKQu0mW4jnC9hA1IC7CPvU2JYHl_AL341KaUu6eyXJI43h_8wzD9k6Jq9rOS_Pb4nXjHEf3Y2PcSp0HsuT_VJsRQ_Xj6L42FhnJy6Ea2yfDtMqTxFgfVR9L-Ubeni4ez54mfly4qXhc5dfwGvvO7VHJfGGZsroLn7nqEctj3tA7SkjMFONpN8K2ef5k0JGW8U_JhqyH4PEK2eeCHsH2bSSK2eOdy6NQpTN59bguMv4ai7-QgqHvJIz_K_plPwgWQTm-8xuSoWoInwFQQy17zArx0mPLu-AoAvfUClMY1WI_mmXgRFHcPinadEM6Iuw
                    kubectl config set-context cfc --user=user --namespace=default
                    kubectl config use-context cfc
                    ls -la
                    kubectl create -f app.json
                    kubectl create -f service.json
                '''
            }
        }
    }
}
