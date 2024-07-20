# CODTECH-Task-1
- Name:Chatla Tharun
- Company:CODTECH IT SOLUTIONS
- ID:CT12DS1611
- Domain:DevOps
- Duration:July to September 2024
- Mentor:SANTHOSH
- # overview of the project
- ## Project: Create a Jenkins continuous integration/continuous deployment(CI/CD) pipeline to build, test, and deploy a application
- **Objectives**
- Automata Build process 
- Automate Testing
- Automate Deploying
- ### Process
- #### step:1
-Login to AWS console
-Headover to EC2 dashboard
-Launch instance
- Name=jenkins
- OS of instance=Ubuntu 
![Screenshot 2024-07-20 223248](https://github.com/user-attachments/assets/a1ca9f75-d4da-4393-8b32-f30467ea804a)
- Type of Instance =t2.large
- create a key pair or select existing key pair                     
![Screenshot 2024-07-20 224026](https://github.com/user-attachments/assets/c4dbcb77-c992-4f41-9fba-be602eacf86b)
- Network setting
- select the VPC,Subnet,Create security group
- by allowing port no:8080(Default jenkins port number),default port number of tomcat is 8080, To avoid conflicts with Jenkins, we are changing the port number of tomcat to 80 and SonarQube port no:9000
- ![Screenshot 2024-07-20 225211](https://github.com/user-attachments/assets/0a785598-17e2-4614-9b97-8a265c6c521d)
- launch the instance
- #### step:2(after launching the instance)
- connect the instance to gitbash using shh client
- ![Screenshot 2024-07-20 230536](https://github.com/user-attachments/assets/1acc7c37-4f3d-4867-af0f-c3ef1b77796b)
- -make it as root user(command=sudo -i or sudo su) , update using (command=apt update -y)
- Install java,maven,jenkins,sonarqube,tomcat
- for java(command=apt install default-jdk -y)
- for maven(command=apt install maven -y)
- for jenkins(command=wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins) ( copy for offical web site )
- for tomcat(wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.91/bin/apache-tomcat-9.0.91.tar.gz) (copy from offical wed site)
- for sonarqube(command=apt install docker.io -y | docker run --name myc1 -d -p 9000:9000 sonarqube:latest)
- ##TOMCAT##
- first untar the tomcat file using command=(tar -xvdf file_name)
- 

