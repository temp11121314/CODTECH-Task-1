# CODTECH-Task-1
- Name:Murivini Venkata Naveen
- Domain:DevOps
- Duration:July to September 2024
- Mentor:VCUBE
# overview of the project
## Project: Create a Jenkins continuous integration/continuous deployment(CI/CD) pipeline to build, test, and deploy a application
# *Objectives*
- Automate Build process 
- Automate Testing
- Automate Deployment
# *Tools*
- Build tools: Maven 
- Testing: SonarQube
- CI/CD tool: Jenkins
- Server: Tomcat
## Process
#### step 1: Setup AWS instance
- Login to AWS console
- Head over to EC2 dashboard
- Launch instance
- Name=jenkins
- OS=Ubuntu 
![Screenshot 2024-07-20 223248](https://github.com/user-attachments/assets/a1ca9f75-d4da-4393-8b32-f30467ea804a)
- Type of Instance: t2.large
- Create a key pair or select existing key pair                     
![Screenshot 2024-07-20 224026](https://github.com/user-attachments/assets/c4dbcb77-c992-4f41-9fba-be602eacf86b)
- Configure Network settings
- Select the VPC,Subnet,Create security group
- By allowing port no:8080(Default jenkins port number),default port number of tomcat is 8080, To avoid conflicts with Jenkins, we are changing the port number of tomcat to 80 and SonarQube port no:9000
  ![Screenshot 2024-07-20 225211](https://github.com/user-attachments/assets/0a785598-17e2-4614-9b97-8a265c6c521d)
- Launch the instance
#### Step 2: Configure the Instance
- Connecting to the instance using SSH client
  ![Screenshot 2024-07-20 230536](https://github.com/user-attachments/assets/1acc7c37-4f3d-4867-af0f-c3ef1b77796b)
- Make it a root user(command=sudo -i or sudo su) , update using (command=apt update -y)
### Step 3: Install java,maven,jenkins,sonarqube,tomcat
#### 1. Java
- To install Java use:
  ```command=apt install default-jdk -y```
#### 2. Maven
- To install Apache Maven use:
 ```apt install maven -y```
#### 3. Jenkins
- To install jenkins
 ```
  sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
  echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
  sudo apt-get update
  sudo apt-get install jenkins
 ```
#### 4. SonarQube
- To install SonarQube using Docker:
  ```
   apt install docker.io -y
   systemctl start docker 
   systemctl enable docker
   docker run --name myc1 -d -p 9000:9000 sonarqube:latest ```
#### 4. Tomcat install and set up
- To install Apache Tomcat:
 ```wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.91/bin/apache-tomcat-9.0.91.tar.gz```
- First untar the tomcat file using command:
- ``` tar -xvzf apache-tomcat-9.0.91.tar.gz && mv apache-tomcat-9.0.91.tar.gz tomcat ```
- Change directory to tomcat and go to conf directory command:(
- ``` cd /tomcat/conf/```
- `vi tomcat-users.xml` here we need to add a user to manage the GUI and script
 ![Screenshot 2024-07-21 101642](https://github.com/user-attachments/assets/1303395a-c849-4c0f-9495-6448eedb3192)
- Change port number of Tomcat by opening server.xml file `vi server.xml` change port no:80
 ![Screenshot 2024-07-21 102624](https://github.com/user-attachments/assets/a255271e-b573-4c98-9db0-07dca7df1792)
- Comment the value in both context.xml files in `cd webapps/manager/META-INF/` `cd /webapps/host-manager/META-INF` To enable the Manager App ![Screenshot 2024-07-21 103159](https://github.com/user-attachments/assets/aca3a73e-fb71-4b67-b9b3-295c6aef3f01)
- To restart the tomcat go to `cd /tomcat/bin` and  `./shutdown.sh` `./startup.sh` then you can view server by copy public ip of instance `52.66.25.109:80`
  ![Screenshot 2024-07-21 104031](https://github.com/user-attachments/assets/7aaa42ed-f293-44c9-b23c-0f8362643634)
### To set up SonarQube
- public ip `52.66.25.109:9000` 9000 is the port number of sonarqube and default credentials for sonarqube is login and password is `admin`
 ![Screenshot 2024-07-21 105118](https://github.com/user-attachments/assets/97fd4436-d6ec-41cc-bcaf-0ac9eeb5deaf)
- Make your own password
 ![Screenshot 2024-07-21 105242](https://github.com/user-attachments/assets/298b56f9-ec14-423f-8b9c-09b544b1df4f)
- Then create local project and name as you like
![Screenshot 2024-07-21 110246](https://github.com/user-attachments/assets/78531fc2-95ce-494b-8ab2-483622dfa78a)
- Use global setting and create project
- After creating project go to Locally for testing
![Screenshot 2024-07-21 110549](https://github.com/user-attachments/assets/e143b469-ecd3-4b73-9215-49cdd4394de1)
- Generate token and maven for run analysis
- then copy the command for running code review
![Screenshot 2024-07-21 110913](https://github.com/user-attachments/assets/633da65a-5cdf-4808-adb1-b557a1117ead)
### To set up Jenkins 
- To open Jenkins server, go to `52.66.25.109:8080`. To get password, Use `cat /var/lib/jenkins/secrets/initialAdminPassword` will get the password and install suggested plugin
 ![Screenshot 2024-07-21 102432](https://github.com/user-attachments/assets/a8a9ac55-8fa9-4e2b-b09b-1b4cef0d9bc6)
- And create Admin by giving you own data then jenkins server is started
 ![Screenshot 2024-07-21 104649](https://github.com/user-attachments/assets/5fa7a8ab-5585-4d6d-bfa9-77476193c637)
- In Manage Jenkins![Screenshot 2024-07-21 112445](https://github.com/user-attachments/assets/11cd51b0-3f0f-48db-8906-d5bc70a2fddc)
- Go to Plugins in available plugins download the 'Deploy to Container' plugin ![Screenshot 2024-07-21 114131](https://github.com/user-attachments/assets/be1a9f98-7783-4de0-90d3-8203f8a8d2fa)
- Go to Credentials and in global add credentials username and password and id:tomcat ![Screenshot 2024-07-21 114640](https://github.com/user-attachments/assets/0fdb2dca-1bdf-4a5e-b721-543458b572de) ![Screenshot 2024-07-21 115109] 
  (https://github.com/user-attachments/assets/53a1aaec-f758-4de6-a88d-67111f96c72e)
- Create new item to build ,test ,deploy application and
- Enter item name:pipeline and select the pipeline ![Screenshot 2024-07-21 111753](https://github.com/user-attachments/assets/c861f244-6798-4f36-b4b1-f4e19eb2a630)
- Then write the pipeline script here ![Screenshot 2024-07-21 112021](https://github.com/user-attachments/assets/b7a20855-ba40-46c6-8454-f58ce5f32419)
- First stage is git clone use the pipeline syntax to generate script![Screenshot 2024-08-10 212523](https://github.com/user-attachments/assets/ec39ac14-59a3-4d0d-995e-193d275eb92b)
- Next stages maven validate and maven compile and maven test
- In the Maven package stage, it converts to a WAR file.
- In sonarqube stage, provide the copy link of the SonarQube command and sonarqube perform static testing
- Then this WAR file is deployed to Tomcat using pipeline script for 'Deploy to Container' ![Screenshot 2024-08-10 212503](https://github.com/user-attachments/assets/4cfd0c45-a1a2-42da-a313-8ca81e117b32)

- The overall script of pipeline
- ### Jenkins Pipeline Script
```groovy
pipeline {
    agent any 
    stages {
        stage('Git Clone') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Venn1991/train-ticket-reservation.git']])
            }
        }
        stage('Maven Validate') {
            steps {
                sh 'mvn validate'
            }
        }
        stage('Maven Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Maven Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('SonarQube Test') {
            steps {
                sh "mvn clean verify sonar:sonar -Dsonar.projectKey=project -Dsonar.projectName='project' -Dsonar.host.url=http://52.73.212.149:9000 -Dsonar.token=sqp_2e29282770245a7a6e20e84289889712d51a2b56"
            }
        }
        stage('maven package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://52.73.212.149')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
```
![Screenshot 2024-08-10 212606](https://github.com/user-attachments/assets/0e4946dd-1cbf-43c1-b883-adf4d7cc8b22)
![Screenshot 2024-08-10 212440](https://github.com/user-attachments/assets/796b264f-70ef-4aa7-bb53-811ec302b5e9)
![Screenshot 2024-08-10 213443](https://github.com/user-attachments/assets/49feec43-126b-4b26-96b2-a498e916afdc)
![Screenshot 2024-08-10 213252](https://github.com/user-attachments/assets/70c946e6-4619-47cd-8d06-acd78e8a44ac)










