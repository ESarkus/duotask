pipeline {
    agent any
    stage 
        stage('Build') {
            steps {
                 sh '''docker build -t esarkus/flask-app:latest
                       docker build -t esarkus/nginx:latest ./nginx
                    '''
                }
        }
        stage('Push') {
            steps {
                        sh '''
                        docker push esarkus/flask-app:latest
                        docker push esarkus/nginx:latest
                        '''
                    } 
                }
        stage('Deploy') {
            steps {
                script {
                        sh'''
                        kubectl apply -f . --namespace=development
                        kubectl rollout restart deployment --namespace=development
                        '''
                    }
                }
            }
    }
