# eks-aks


#Install the JAVA
yum install java-11*

#Find the java installation 
find / -name java-11* | head -n 4
------------------------------------------------------------------------------------------------
/**
cat  << 'EOF' >> ~/.bash_profile
###################################
#.bash_profile
#Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

#JAVA HOME Path setting 
JAVA_HOME=/usr/lib/jvm/java-11-amazon-corretto.x86_64
export JAVA_HOME

#Maven path setting
export M2_HOME=/opt/apache-maven-3.9.6
export M2=$M2_HOME/bin

#User specific environment and startup programs
PATH=$PATH:$HOME/bin:$JAVA_HOME:$M2
export PATH


#Updated by hari
#########################################
EOF
**/

--------------------------------------------------------
#Java Version check 

java -version


#jenking instllation 

echo " Updating the Jankins instllation "

wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

yum -y install jenkins

systemctl enable jenkins

systemctl start jenkins


#add the security group 
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version


# instllation of git 

yum install git -y 


# Maven installation

cd /opt
wget https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz

tar -xzvf apache-maven-3.9.6-bin.tar.gz
rm -rf apache-maven-3.9.6-bin.tar.gz

# validate Mavin

mvn version

# Assign shell to jenkins user

#vi /etc/passwd
#change shell from /bin/false to /bin/bash


# Docker installation 

yum install docker -y

systemctl start docker 
systemctl enable docker 

sudo groupadd docker
sudo usermod -aG docker jenkins
sudo chmod 777 /var/run/docker.sock





#### EKS - managed servers 

#AWS CLI instllation 
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
 aws --version

#Kubectl instllation 

kubectl version --client
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.28.3/2023-11-14/bin/linux/amd64/kubectl
chmod +x ./kubectl
mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH
echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
kubectl version --client


#aws eks update-kubeconfig --region region-code --name my-cluster

#eksctl instllation 

# for ARM systems, set ARCH to: `arm64`, `armv6` or `armv7`
ARCH=amd64
PLATFORM=$(uname -s)_$ARCH

curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"

# (Optional) Verify checksum
curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check

tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm -rf eksctl_$PLATFORM.tar.gz

sudo mv /tmp/eksctl /usr/local/bin

eksctl -version


####

# update the IAM roles for both servers :
-> attache the below roles 
 1. cloudformation
 2. EC2full
 3. IAM full
 4. eks full
 5. 

## install the EKS nodes - 

https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html#eksctl-prereqs

# Nodes 

# Fargate 

# Docker hub registory user id and pass word 
#Docker Hub
#lhksre@gmail.com#harikrishna415


















