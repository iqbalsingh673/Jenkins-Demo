pipeline {
     agent any
     stages {
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }
         stage('Build Docker Image') {
              steps {
                  sh 'docker build -t udacity_capstone .'
              }
         }
         stage('Push Docker Image') {
              steps {
                  withDockerRegistry([url: "", credentialsId: "DockerHub"]) {
                      sh "docker tag udacity_capstone iqbalsingh673/udacity_capstone"
                      sh 'docker push iqbalsingh673/udacity_capstone'
                  }
              }
         }
         stage('Deploying docker container') {
              steps{
                  echo 'Deploying to AWS...'
                  withAWS(credentials: 'aws-static', region: 'us-east-2') {
                      sh "aws eks --region us-east-2 update-kubeconfig --name UdacityCapstone"
                      sh "kubectl apply -f deployment.yml"
		      sh "sleep 2m"
                      sh "kubectl rollout status deployment.v1.apps/udacity_capstone-deployment"
		      sh "kubectl get deployment"
		      sh "kubectl get rs"
                      sh "kubectl get pods"
                      sh "kubectl get svc"
                  }
              }
        }
        stage('Rolling Deployment') {
              steps{
                  echo 'Deploying to AWS...'
                  withAWS(credentials: 'eksuser', region: 'us-east-1') {
                      sh "kubectl set image deployments/udacity_capstone-deployment udacity_capstone=iqbalsingh673/udacity_capstone:latest"
		      sh "sleep 2m"
                      sh "kubectl rollout status deployment.v1.apps/udacity_capstone-deployment"
		      sh "kubectl get deployment"
                      sh "kubectl get rs"
                      sh "kubectl get pods"
                      sh "kubectl get svc"
                  }
              }
        }
     }
}
