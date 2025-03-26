# Micro-Service-deployment
End to End DevOps Implementation on an E-Commerce project 
THE GITHUB FOR THIS PROJECT IS
https://github.com/iam-veeramalla/ultimate-devops-project-demo

Documentation
https://opentelemetry.io/docs/demo/architecture/


INSTALLATIONS AND PREREQUISTES

Steps
1. Login into AWS ACCOUNT
2. Create an EC2 instance choose (India region) and
3. select  instance Type as (t2.large), ALSO use 30gb size not 8gb size when creating the EC2 instance 

￼


￼



1. Login from Terminal
       ssh -I devops.pem ubuntu@123.345.456
     Remember  you have to use Key gen and IP of the Instance you generated

YOU HAVE TO INSTALL 
	Ducker
	KUBECTL
	TERRAFORM

Steps to install 3 Application in Your Running Server 
NEXT 
1. Install Docker
	https://docs.docker.com/engine/install/ubuntu/
	
The link Above is the officer website of ubuntu, you can see the step to install


sudo apt-get update

sudo apt-get install ca-certificates curl

sudo install -m 0755 -d /etc/apt/keyrings

sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

sudo chmod a+r /etc/apt/keyrings/docker.asc


 Add the repository to Apt sources: Run below cold 

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update



sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo docker run hello-world

docker ps     ( you get docker denied)

Grant access to ubuntu
sudo usermod -aG docker ubuntu

sudo docker ps (you get positive result)

docker ps
logout

ssh -I devops-demo.pem ubuntu@123.4657.98


Run without sudo just docker ps
docker ps
docker images


NEXT INSTALLATION

1. Install Kubectl
	https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-kubectl-binary-with-curl-on-linux
What is kublectl? GOOGLE THIS 

Step to install below

	curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

RUN 
ls     ( you will see kubectl)


Validate the binary RUN
   	curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"


Validate the kubectl binary against the checksum file RUN
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

RUN
 ls
(You will see kubectl & kubectl.sha

Install kubectl RUN
	sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
	kubectl version --client


Step to install Terraform

1. Install Terraform
	https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

	sudo apt-get update && sudo apt-get install -y gnupg software-properties-common

	
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null

	
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint


echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list


sudo apt update


sudo apt-get install terraform


terraform -help
terraform --version



WITH THE SAME VM CONTINUE



PART 2
HOW TO RUN  PROJECT LOCALLY

Steps

CHECK IF DOCKER IS INSTALLED
docker compose -h

CLONE THE REPO FROM GITHUB

git clone  https://github.com/iam-veeramalla/ultimate-devops-project-demo
CHANGE THE DIRECTORY TO ultimate-devops-project-demo
cd ultimate-devops-project-demo
docker compose up -d


AFTER THE GIT CLONE IS COMPLETED GO BACK TO AWS WEBSITE OPEN PORT 8080 

THEN PASTE YOUR IP ADDRESS WITH THE PORT ADDED 8080 
EXAMPLE MY IP AND PORT
123.4657.98:8080 
YOU SEE THE WEBSITE


DIAGRAM OF MICROSERVICE 
￼

From the Micro-Service
Choose product catalog
Steps
cd ultimate-devops-project-demo
ls
cd src
You will all the Micro Service build by developers

accounting  currency  fraud-detection  image-provider  payment          react-native-app
ad          email     frontend         kafka           product-catalog  recommendation
cart        flagd     frontend-proxy   load-generator  prometheus       shipping
checkout    flagd-ui  grafana          otel-collector  quote


GO TO https://github.com/iam-veeramalla/ultimate-devops-project-demo
SCR
PRODUCT-CATALOG
README-FILE

git clone  https://github.com/iam-veeramalla/ultimate-devops-project-demo
cd ultimate-devops-project-demo
cd src
cd product-catalog/

COPY THIS CODE FROM README ON GITHUB OF THIS REPOSITORY
export PRODUCT_CATALOG_PORT=8080

INSTALL GOLAND ON YOUR CURRENT SERVER
sudo apt update
sudo apt install golang-go
go build -o product-catalog . 
ls -ltr
./product-catalog

This step help you how to build the go binary locally on your machine.
 
￼
THE life cycle of Docker
Steps
Create docker file
build dockerfile
Run the Docker images
Will Containerize 



CONTAINERIZATION OF FIRST MICROSERVICE - PRODUCT CATALOG -GOLANG

Steps

git clone  https://github.com/iam-veeramalla/ultimate-devops-project-demo
cd ultimate-devops-project-demo
cd src
cd product-catalog
cd scr
ls


TO BUILD THE DOCKER FILE RUN
docker build -t tonymore/product-catalog:v1 .
docker images | grep tonymore
docker run tonymore/product-catalog:v1




STEP 2
CONTAINERIZED A JAVA BASED MICROSERVICE Ad

git clone  https://github.com/iam-veeramalla/ultimate-devops-project-demo
cd ultimate-devops-project-demo
cd src
cd ad
ls

GO TO GITHUB README FILE FOR AD TO SEE HOW TO EXECUTE IT BY THE DEVELOPER
https://github.com/iam-veeramalla/ultimate-devops-project-demo/blob/main/src/ad/README.md

 

RUN
java —version 
sudo apt install openjdk-21-jre-headless 

./gradlew
chmod +x ./gradlew
./gradlew installDist
	what this command will do
Install Bradley deomon
Install dependence
Compilation
Build

RUN
ls -ltr  
To  See if build is on the list

RUN 
ls -ltr ./build/install/opentelemetry-demo-ad/bin/Ad
export AD_PORT=9099                      (Change the port of your choice )

export FEATURE_FLAG_GRPC_SERVICE_ADDR=featureflagservice:50053

./build/install/opentelemetry-demo-ad/bin/Ad

YOU SEE SOME LOGS MEANS THE BUILD IS BUILD SUCCESSFULLY


STEP TO RUN THE DOCKERFILE 
THE life cycle of Docker
Steps
Create docker file
build dockefile
Run the Docker images
Will Containerize


nano Dockerfile
YOU SEE THE  FILE INSIDE THE DOCKERFILE

docker build -t tonymore/adservice:v1 .
docker run tonymore/adservice:v1




STEP 3
CONTAINERIZED A PYTHON BASED MICROSERVICE RECOMMENDATION

git clone  https://github.com/iam-veeramalla/ultimate-devops-project-demo
cd ultimate-devops-project-demo
cd src
cd recommendation
ls

GO TO GITHUB README FILE FOR AD TO SEE HOW TO EXECUTE IT BY THE DEVELOPER
https://github.com/iam-veeramalla/ultimate-devops-project-demo/blob/main/src/recommendation/README.md

TO SEE THE CODE TO RUN IT LOCALLY IF YOU FIND THE DOCKERFILE INSIDE THESE FOLDER THE YOU RUN THE DOCKERFILE AFTER FIRST RUNNING IT LOCAL ON YOUR MACHINE 

IN MY CASE I MAKE USED OF THE DOCKERFILE

BUILD THE Dockerfile
docker build -t tonymore/recommendationservice:v1 .

RUN THE Dockerfile
docker run tonymore/recommendationservice:v1






