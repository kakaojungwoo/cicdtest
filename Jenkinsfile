pipeline {
    agent any
    stages {
        stage ('git update') {
          steps {
            git url: 'https://github.com/kakaojungwoo/cicdtest.git', branch: 'main'
          }
        }
        stage ('docker build and push') {
          steps {
            sh '''
            sudo docker build -t oncliff/cicdtest:jenkins .
            sudo docker push oncliff/cicdtest:jenkins
            '''
          }
        }
        stage('deploy kubernetes') {
          steps {
            sh '''
            ansible master -m command -a 'kubectl create deployment jenkinstest --image=oncliff/cicdtest:jenkins'
            ansible master -m command -a 'kubectl expose deployment jenkinstest --type=LoadBalancer --port=80 --target-port=80 --name=jenkinstest'
            
            '''
          }
        }
    }
}      
