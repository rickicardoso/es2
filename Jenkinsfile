def dockeruser = "40404040"
def imagename = "ubuntu:16"
def container = "apache2"
node {
   echo 'Building Apache Docker Image'

stage('Git Checkout') {
    git 'https://github.com/jvpreis/ESII'
    }
    
stage('Build Docker Imagae'){
     powershell "docker build -t  ${imagename} ."
    }
    
stage('Stop Existing Container'){
     powershell "docker stop ${container}"
    }
    
stage('Remove Existing Container'){
     powershell "docker rm ${container}"
    }
    
stage ('Runing Container to test built Docker Image'){
    powershell "docker run -dit --name ${container} -p 80:80 ${imagename}"
    }
    
stage ('Build') {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }

}
