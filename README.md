# Task---2
CI/CD PIPELINE SETUP
Open Aws and open EC-2 Instance and start a Instance.
Connect .ssh to the putty.
Using Amazon Linux as operating sysytem.
Update the drivers and install java.
Run commands--
  sudo amazon-linux-extras install java-openjdk11
  sudo yum install java-1.8.0-openjdk
  java -version..
These are the above commands to install java now install jenkins.
Run commands to install jenkins--
  sudo yum install jenkins -y
  sudo systemctl start jenkins
  sudo systemctl enable jenkins
http://<387.5.7.8>:8080.  
<img width="669" alt="jenkins dashboard" src="https://github.com/user-attachments/assets/017e100f-25df-4500-9865-c01e6ac6f9dc" />
sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Use this command in amazon linux to show the password to access jenkins.
Go to plugins and install the neccesary docker and maven plugins.
Go to Jenkins Dashboard → New Item → Pipeline.
Go to Manage Jenkins → Configure System.
Add GitHub plugin and link your GitHub repository (where your web application’s code is hosted).
If needed, generate a GitHub token for Jenkins to access your GitHub repository securely.
Jenkins pipeline---
pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-user/your-repo.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Install dependencies and build your app
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    // Run tests for your app
                    sh 'npm test'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Deploy your app using AWS CLI or CodeDeploy
                    sh """
                        aws s3 cp ./build/ s3://your-bucket-name/ --recursive
                        aws deploy create-deployment --application-name your-app-name --deployment-group-name your- 
                        deployment-group --revision revisionType=S3, S3Location={bucket=your-bucket-name,key=your- 
                        artifact.zip}
                    """
                }
            }
        }
    }
}

--------------------------------------------------------------------------------------------
Install AWS CLI--
  sudo yum install aws-cli -y
Install Node.js
   sudo yum install nodejs -y
   sudo npm install pm2 -g 

