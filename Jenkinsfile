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
                  sh 'docker build -t vibcapstoneapp .'
              }
         }
         stage('Push Docker Image') {
              steps {
                  withDockerRegistry([url: "", credentialsId: "dockerhubuser"]) {
                      sh "docker tag vibcapstoneapp vibhore68/vibcapstoneapp"
                      sh 'docker push vibhore68/vibcapstoneapp'
                  }
              }
         }
         stage('Deploying docker container') {
              steps{
                  echo 'Deploying to AWS...'
                  withAWS(credentials: 'eksuser', region: 'us-east-1') {
                      sh "aws eks --region us-east-1 update-kubeconfig --name CapstoneEKS-g41IEceOgaS7"
                      sh "kubectl apply -f deployment.yml"
		      sh "sleep 8m"
                      sh "kubectl rollout status deployment.v1.apps/vibcapstoneapp-deployment"
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
                      sh "kubectl set image deployments/vibcapstoneapp-deployment vibcapstoneapp=vibhore68/vibcapstoneappv2:latest"
		      sh "sleep 8m"
                      sh "kubectl rollout status deployment.v1.apps/vibcapstoneapp-deployment"
		      sh "kubectl get deployment"
                      sh "kubectl get rs"
                      sh "kubectl get pods"
                      sh "kubectl get svc"
                  }
              }
        }

}
