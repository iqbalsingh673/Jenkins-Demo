# Udacity-Cloud-Devops-Capstone
Udacity Cloud Devops Capstone Project

<h2>Project Overview</h2>

<p> In this project, I applied the skills and knowledge which was developed throughout the Cloud DevOps Nanodegree program. These include:</p>

<p>I developed a CI/CD pipeline for Nignx Hello world application with rolling deployment. I developed Continuous Integration steps, such as linting. I also developed Contiguous Deployment steps. The pipeline steps include:</p>

<ul>
	<li>Linting the code</li>
	<li>Building docker image from Dockerfile</li>
	<li>Pushing docker image to Dockerhub</li>
	<li>Deploying image to Kubernetes Cluster</li>
	<li>Deploying the another version of app through Rolling Deployment Strategy</li>
</ul>


<h2>Environment Setup</h2>

<ul>
  <li>Launched Jenkins server - Installed Java, Jenkins, Docker, AWS CLI, Kubectl and tidy</li>
  <li>Created network infrasture for cluster through CloudFormation</li>
  <li>Created for cluster through CloudFormation</li>
  <li>Created Dockerfile for docker imaged</li>
  <li>Ctreated Jenkins CI/CD pipeline</li>
</ul>


<h2>Directory Structure</h2>

<pre>
	<code>
		Screenshots folder - Having the screenshots for the deployment
		Jenkinsfile - to setup CI/CD pipeline
		Dockerfile - To create docker image for deployment
		index.html - Nginx hello world html app
		infra.yml - Cloudformation YAML for creating network infrastructure
		infra-params.json - parameter json file for network infrastructure
		eks-cluster.yml - Cloudformation YAML for craeting cluster
		eks-cluster-params.json - parameter json file for cluster
		amazon-eks-nodegroup.yml - Cloudformation YAML for worker nodes
		amazon-eks-nodegroup-params.json - parameter json file for worker nodes
	</code>
</pre>


