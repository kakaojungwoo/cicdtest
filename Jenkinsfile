pipeline {
    agent any
    stages {
        stage ('git update') {
          steps {
            git url: 'https://github.com/kakaojungwoo/cicdtest.git'
          }
        }
        stage ('docker build and push') {
          steps {
            sh '''
            docker build -t oncliff/cicdtest:blue .
            docker push oncliff/cicdtest:blue
            '''
          }
        }
        stage('deploy kubernetes') {
          steps {
            sh '''
            ansible master -m command -a kubectl create deployment jenkinstest --image=oncliff/cicdtest:blue
            ansible master -m command -a kubectl expose deployment jenkinstest --type=LoadBalancer --port=80 --target-port=80 --name=jenkinstest
            
            '''
          }
        }
    }
}      
