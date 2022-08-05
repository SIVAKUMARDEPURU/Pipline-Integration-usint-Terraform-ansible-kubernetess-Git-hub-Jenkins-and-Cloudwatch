# CI/CD pipeline integration by using terraform, ansible,kubernetes,Jenkins,cloudwatch
############################...SIVAKUMAR DEPURU...###################################
                        Install kubectl and kops
 kubectl install Steps:

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
kubectl version --client

kops Install Steps:
curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
curl -LO https://github.com/kubernetes/kops/releases/download/v1.20.0/kops-linux-amd64
chmod +x kops-linux-amd64
sudo mv kops-linux-amd64 /usr/local/bin/kops

#route53 and cluster forming
aws s3 mb s3://clusters.cicd.in
export KOPS_STATE_STORE=s3://clusters.cicd.in
kops create cluster --cloud=aws --zones=us-east-1a --name=clusters.cicd.in --dns-zone=cicd.in --dns private
kops update cluster clusters.cicd.in --yes --admin
kops validate cluster
kubectl get nodes 

Installation Steps :
Please launch an Amazon Linux instance using Amazon Linux AMI.
Login to your Amazon Linux instance.
Become root using “sudo su -” command.
Update your repositories
yum update
yum install java
Get Jenkins repository using below command
wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
Get Jenkins repository key
rpm --import http://pkg.jenkins-ci.org/redhat-stable/jenkins-ci.org.key
Install jenkins package
yum install jenkins
Start jenkins and make sure it starts automatically at system startup
Systemctl start jenkins
Systemctlenable jenkins
yum install git
Ansible Server Configuration{ Ansible}
Amazon linux install ansible2
