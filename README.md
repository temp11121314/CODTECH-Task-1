# CODTECH-Task-1
- Name:Chatla Tharun
- Company:CODTECH IT SOLUTIONS
- ID:CT12DS1611
- Domain:DevOps
- Duration:July to September 2024
- Mentor:SANTHOSH
- # overview of the project
- ## Project: Create a Jenkins continuous integration/continuous deployment(CI/CD) pipeline to build, test, and deploy a application
- # *Objectives*
- Automata Build process 
- Automate Testing
- Automate Deploying
- Build tools=Maven
- Testing=SonarQube
- CI/CD tool=Jenkins
- Server=Tomcat
- ### Process
- #### step:1
-Login to AWS console
-Headover to EC2 dashboard
-Launch instance
- Name=jenkins
- OS of instance=Ubuntu 
![Screenshot 2024-07-20 223248](https://github.com/user-attachments/assets/a1ca9f75-d4da-4393-8b32-f30467ea804a)
- Type of Instance =t2.large
- Create a key pair or select existing key pair                     
![Screenshot 2024-07-20 224026](https://github.com/user-attachments/assets/c4dbcb77-c992-4f41-9fba-be602eacf86b)
- Network setting
- Select the VPC,Subnet,Create security group
- By allowing port no:8080(Default jenkins port number),default port number of tomcat is 8080, To avoid conflicts with Jenkins, we are changing the port number of tomcat to 80 and SonarQube port no:9000
- ![Screenshot 2024-07-20 225211](https://github.com/user-attachments/assets/0a785598-17e2-4614-9b97-8a265c6c521d)
- Launch the instance
- #### step:2(after launching the instance)
- Connect the instance to gitbash using shh client
- ![Screenshot 2024-07-20 230536](https://github.com/user-attachments/assets/1acc7c37-4f3d-4867-af0f-c3ef1b77796b)
- Make it as root user(command=sudo -i or sudo su) , update using (command=apt update -y)
- ### Install java,maven,jenkins,sonarqube,tomcat
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
- ##TOMCAT
- First untar the tomcat file using command=(tar -xvdf file_name)
- Change directory to tomcat and go to conf directory command=(cd /tomcat/conf/)
- vi tomcat-users.xml (here we need to add user to manage-gui and script)
- ![Screenshot 2024-07-21 101642](https://github.com/user-attachments/assets/1303395a-c849-4c0f-9495-6448eedb3192)
- Change port number of tomcat by opening server.xml file(vi srever.xml) change prot no:80
- ![Screenshot 2024-07-21 102624](https://github.com/user-attachments/assets/a255271e-b573-4c98-9db0-07dca7df1792)
- Make the value to comment in context.xml files in (cd webapps/manager/META-INF/) (cd /webapps/host-manager/META-INF)
-![Screenshot 2024-07-21![Screenshot 2024-07-21 105242](https://github.com/user-attachments/assets/83fb6461-ad56-4732-ba91-3898db1e9ce3)
 103159](https://github.com/user-attachments/assets/59499307-3b6a-4294-8281-ad8ebee94af0)
- Then restart the tomcat by (cd /tomcat/bin) and ./shutdown.sh) (./startup.sh) then you can view sever by copy public ip of instance (52.66.25.109:80)
  ![Screenshot 2024-07-21 104031](https://github.com/user-attachments/assets/7aaa42ed-f293-44c9-b23c-0f8362643634)
- ## To setup sonarqube
- public ip (52.66.25.109:9000) 9000 is the port number of sonarqube and default credentials for sonarqube is login and password is admin
- ![Screenshot 2024-07-21 105118](https://github.com/user-attachments/assets/97fd4436-d6ec-41cc-bcaf-0ac9eeb5deaf)
- Make you own password
- ![Screenshot 2024-07-21 105242](https://github.com/user-attachments/assets/298b56f9-ec14-423f-8b9c-09b544b1df4f)
- Then create local project and name as you like ![Screenshot 2024-07-21 105242](https://github.com/user-attachments/assets/63368f1b-b3e1-4e7d-8ea3-07b40c8d51f8)
- Use global setting and create project ![Screenshot 2024-07-21 110246](https://github.com/user-attachments/assets/c06c0d13-ac9b-4bfb-87f8-60abc5372f31)
- After creating project go to Locally for testing ![Screenshot 2024-07-21 110549](https://github.com/user-attachments/assets/7da8bfbf-f74f-4294-a5d1-25af16df0e1f)
- Token generate and select maven for run analysis![Screenshot 2024-07-21 110913](https://github.com/user-attachments/assets/633da65a-5cdf-4808-adb1-b557a1117ead)
- then copy the command for running code review
- ## Jenkins 
- To open jenkins server 52.66.25.109:8080 for password cat /var/lib/jenkins/secrets/initialAdminPassword will get the password and install suggested plugins
- ![Screenshot 2024-07-21 102432](https://github.com/user-attachments/assets/a8a9ac55-8fa9-4e2b-b09b-1b4cef0d9bc6)
- And create Admin by giving you own data then jenkins server is started
- ![Screenshot 2024-07-21 104649](https://github.com/user-attachments/assets/5fa7a8ab-5585-4d6d-bfa9-77476193c637)
- In manage jenkins![Screenshot 2024-07-21 112445](https://github.com/user-attachments/assets/11cd51b0-3f0f-48db-8906-d5bc70a2fddc)
- Go to Plugins in available plugins download the deploy to container ![Screenshot 2024-07-21 114131](https://github.com/user-attachments/assets/be1a9f98-7783-4de0-90d3-8203f8a8d2fa)
- GO to credentials and in global add credentials username and password and id:tomcat ![Screenshot 2024-07-21 114640](https://github.com/user-attachments/assets/0fdb2dca-1bdf-4a5e-b721-543458b572de) ![Screenshot 2024-07-21 115109](https://github.com/user-attachments/assets/53a1aaec-f758-4de6-a88d-67111f96c72e)
- Create new item to build ,test ,deploy application and
- Enter item name:pipeline and select the pipeline ![Screenshot 2024-07-21 111753](https://github.com/user-attachments/assets/c861f244-6798-4f36-b4b1-f4e19eb2a630)
- Then write the pipeline script here ![Screenshot 2024-07-21 112021](https://github.com/user-attachments/assets/b7a20855-ba40-46c6-8454-f58ce5f32419)
- First stage is git clone use the pipeline syntax to generate script![Screenshot 2024-07-21 143855](https://github.com/user-attachments/assets/20c34bc1-bf25-469a-9801-adcb0e013b19)
- Next stages maven validate and maven compile
- In test stage give the copy line of sonarqube command
- In maven package it convert to var file
- Then this var file is deployed to tomcat using pipeline script for deploy to container ![Screenshot 2024-07-21 142505](https://github.com/user-attachments/assets/e0ae4d7b-d11c-4c5b-9bb2-be1349bb8034)
- The overall script of pipeline ![Screenshot 2024-07-21 144417](https://github.com/user-attachments/assets/490d7139-3ab7-46cd-bc06-1eff8a8e395c)
 







