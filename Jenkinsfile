pipeline{
        agent any
        stages{
            stage('Clone Repository'){
                steps{
                    sh "git clone https://gitlab.com/qacdevops/chaperootodo_client"
                    sh "cd chaperootodo_client"
                }
            }
            stage('install Docker'){
                steps{
                    sh "sudo apt-get update"
                    sh "sudo apt install curl -y"
                    sh "curl https://get.docker.com | sudo bash"
                    sh "sudo usermod -aG docker jenkins"
                    sh "sudo reboot"
                }
            }
            stage('install Docker-Compose'){
                steps{
                    sh "sudo apt update"
                    sh "sudo apt install -y jq"
                    sh "version=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r '.tag_name')"
                    sh "sudo curl -L 'https://github.com/docker/compose/releases/download/${version}/docker-compose-$(uname -s)-$(uname -m)' -o /usr/local/bin/docker-compose"
                    sh "sudo chmod +x /usr/local/bin/docker-compose"
                }
            }
            stage('Deploy'){
                environment { 
                DB_PASSWORD = 'pino'
            }
                steps{
                    sh "sudo docker-compose pull && sudo -E DB_PASSWORD=${DB_PASSWORD} docker-compose up -d"
                }
            }

        }
}
