pipeline{
        agent any
        enviroment {
            DB_PASSWORD=credentials('db_password')
        }
        stages{
            stage('Clone down git'){
                steps{
                    sh 'rm -rf chaperootodo_client'
                    sh "git clone https://gitlab.com/qacdevops/chaperootodo_client"
                    sh "cd chaperootodo_client"
                }
            }
            stage('Install Docker & Docker-Compose'){
                steps{
                    sh "sudo apt-get update"
                    sh "sudo apt install curl -y"
                    sh "curl https://get.docker.com | sudo bash"
                    sh "sudo username -ah docker (whoami)"
                    sh "sudo apt update"
                    sh "sudo apt install -y curl jq"
                    sh 'sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose'
                    sh "sudo chmod +x /usr/local/bin/docker-compose"
                    sh "sudo usermod -aG docker jenkins"

                }
            }
            stage('Deploy Compose'){
                steps{
                    sh "sudo docker-compose pull && sudo -E DB_PASSWORD=${DB_PASSWORD} docker-compose up -d."
                }
            }
        }
}
