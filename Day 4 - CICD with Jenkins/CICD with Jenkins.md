# Day 4

# CI/CD with Jenkins

## Pipeline Jenkins Frontend, Github Webhook Plugin Integration, dan Jenkins Job Notification 

1. Tambahkan file baru bernama Jenkinsfile ke dalam repository dumbflix-frontend

```
def branch = "master"
def remoteurl = "https://github.com/malikalrizky/dumbflix-frontend.git"
def remotename = "jenkins-fe"
def workdir = "~/dumbflix-frontend/"
def ip = "116.193.191.120"
def username = "kelompok1"
def imagename = "dumbways-fe"
def sshkeyid = "app-server"
def dockerusername = "malikalrk"

pipeline {
    agent any

    stages {
        stage('Pull From Frontend Repo') {
            steps {
                sshagent(credentials: ["${sshkeyid}"]) {
                    sh """
                        ssh -l ${username} ${ip} <<pwd
                        cd ${workdir}
                        git remote add ${remotename} ${remoteurl} || git remote set-url ${remotename} ${remoteurl}
                        git pull ${remotename} ${branch}
                        pwd
                        hostname
                        pwd
                    """
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sshagent(credentials: ["${sshkeyid}"]) {
                    sh """
                        ssh -l ${username} ${ip} <<pwd
                        cd ${workdir}
                        docker build -t ${imagename}:${env.BUILD_ID} .
                        pwd
                    """
                }
            }
        }

        stage('Deploy Image') {
            steps {
                sshagent(credentials: ["${sshkeyid}"]) {
                    sh """
                        ssh -l ${username} ${ip} << pwd
                        cd ${workdir}
                        docker compose down
                        docker tag ${imagename}:${env.BUILD_ID} ${imagename}:latest
                        docker compose up -d
                        pwd
                    """
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sshagent(credentials: ["${sshkeyid}"]) {
                        sh """
                                ssh -l ${username} ${ip} <<pwd
                                docker tag ${imagename}:${env.BUILD_ID} ${dockerusername}/${imagename}:${env.BUILD_ID}
                                docker tag ${imagename}:latest ${dockerusername}/${imagename}:latest
                                docker image push ${dockerusername}/${imagename}:latest
                                docker image push ${dockerusername}/${imagename}:${env.BUILD_ID}
                                docker image rm ${dockerusername}/${imagename}:latest
                                docker image rm ${dockerusername}/${imagename}:${env.BUILD_ID}
                                docker image rm ${imagename}:${env.BUILD_ID}
                                pwd
                        """
                }
            }
        }

        stage('Send Success Notification') {
            steps {
                sh """
                    curl -X POST 'https://api.telegram.org/bot${telegramapi}/sendMessage' -d \
                    'chat_id=${telegramid}&text=Build ID #${env.BUILD_ID} Frontend Pipeline Successful!'
                """
            }
        }
 }
}
```

2. Buat Pipeline

![](/media/day4/Screenshot%20(144).png)

![](/media/day4/Screenshot%20(152).png)

```
- Definition : Pipeline script from SCM
- SCM : Git
- Repository URL : https://github.com/malikalrizky/dumbflix-frontend.git
- Branches : */master
- Script Path : Jenkinsfile
```

3. Pada Repository Github, buka settings dan tambahkan webhook

![](/media/day4/Screenshot%20(154).png)

4. Buat bot telegram dan tambahkan API pada pipeline

![](/media/day4/Capture.JPG)

5. Build Pipeline

![](/media/day4/Screenshot%20(151).png)